# 交付物卫生 · Delivery Hygiene

> 来自 embodied_ai_2026 项目从 v1 → v6 + PPT 实验 + 推 GitHub 的完整教训。报告写完只是 50% 的工作；HTML 渲染、PPT 转换、版本管理、仓库推送都可能在最后一公里把质量毁掉。

---

## 1. HTML 报告：结构性安全

### 1.1 永远不要用正则改 HTML 结构

```python
# ❌ 致命反例（真实事故）：v6 自动审计里写过这行，破坏了 line 332/303 的 div 闭合
html = re.sub(r'  +', ' ', html)

# ✅ 正解：用 DOM 解析器
from bs4 import BeautifulSoup
soup = BeautifulSoup(html, 'html.parser')
# ... 操作 DOM
out = str(soup)
```

正则可以用的场景：
- 注释文本 (`<!-- xxx -->` 里的纯文本)
- 不带标签的字符串属性值（小心 escape）

正则**禁用**的场景：
- 任何会跨越标签边界的替换
- 空白压缩 / 重整缩进
- 标签替换 / 属性重写

### 1.2 保存 HTML 前后必跑 div balance check

```python
from html.parser import HTMLParser

class DivBalance(HTMLParser):
    def __init__(self):
        super().__init__()
        self.opens = 0
        self.closes = 0
        self.stack = []
        self.unbalanced = []
    def handle_starttag(self, tag, attrs):
        if tag == 'div':
            self.opens += 1
            self.stack.append((tag, self.getpos()))
    def handle_endtag(self, tag):
        if tag == 'div':
            self.closes += 1
            if self.stack and self.stack[-1][0] == 'div':
                self.stack.pop()
            else:
                self.unbalanced.append(('extra-close', self.getpos()))

def check(html_path):
    c = DivBalance()
    c.feed(open(html_path).read())
    assert c.opens == c.closes, f"DIV MISMATCH: {c.opens} open / {c.closes} close"
    print(f"OK: {c.opens} balanced")
```

把这个脚本作为 pre-save hook 或 git pre-commit hook。

### 1.3 section 级独立 balance

把每个 `<section>` 单独喂 parser，验证每段 self-contained：

```python
import re
sections = re.findall(r'<section[^>]*id="([^"]+)"[^>]*>(.*?)</section>', html, re.S)
for sid, body in sections:
    c = DivBalance(); c.feed(body)
    if c.opens != c.closes:
        print(f"BROKEN section: #{sid}")
```

### 1.4 视觉验证：Playwright 取多 section 截图

```python
from playwright.async_api import async_playwright
import asyncio

async def screenshot(html_abs_path, sections, out_dir):
    async with async_playwright() as p:
        b = await p.chromium.launch()
        page = await b.new_page(viewport={"width": 1440, "height": 900})
        await page.goto(f"file://{html_abs_path}", wait_until="load", timeout=60000)
        await page.wait_for_timeout(3000)  # let chart.js / mermaid render
        for sid in sections:
            await page.evaluate(f'document.getElementById("{sid}").scrollIntoView()')
            await page.wait_for_timeout(500)
            await page.screenshot(path=f"{out_dir}/{sid}.png", full_page=False)
        await b.close()
```

**关键 flag**：
- `wait_until="load"` 不要 `networkidle`（CDN 永远不 idle）
- 等 3s 给 Chart.js / Mermaid 渲染时间
- 必要时 `await page.wait_for_selector("canvas")`

---

## 2. PPT 转换：保留 HTML 资产

### 2.1 决策树

| 状态 | 选择 |
|---|---|
| 没有 HTML 报告 | 从零写 PPT（用 pptx-from-layouts skill 或 pptxgenjs） |
| 有 HTML + 用户要 PPT + 不重视编辑性 | **截图嵌入**：Playwright 截图 → pptx 插图 |
| 有 HTML + 用户要 PPT + 需要二次编辑 | **重建**：提取 Chart.js 数据 → pptx native chart |
| 有 HTML + 用户重视视觉 | **以 HTML 为主交付**，PPT 仅做摘要版（≤ 15 页） |

### 2.2 PPT 密度规则（来自用户反馈）

- 每页 ≥ 1 个图表 / 表格 / 图标矩阵——**禁纯文字页**
- 信息单元基线：标题 + 3-5 个支撑点 + 1 个 viz
- HTML 一个 section ≈ 1-2 页 PPT，**不允许"一页拆几页"**
- 默认页数：25-40 页，不是 70+ 页
- 标题层级：核心论断写在标题上（"机器人 2027 PMF"），不是"行业概述"这种空标题

### 2.3 截图嵌入路线代码片段

```python
from pptx import Presentation
from pptx.util import Inches

prs = Presentation()
prs.slide_width = Inches(13.333); prs.slide_height = Inches(7.5)  # 16:9
blank = prs.slide_layouts[6]

for png in section_pngs:
    slide = prs.slides.add_slide(blank)
    slide.shapes.add_picture(png, Inches(0.2), Inches(0.2),
                             width=Inches(12.9), height=Inches(7.1))
prs.save('deck.pptx')
```

注意：单张 PNG 全屏铺时，原 HTML 要先按 PPT 比例排版（1920×1080 或 1280×720），不然会留白或失真。

---

## 3. 版本管理与仓库推送

### 3.1 推送前 checklist

```bash
# 1. 看远端有什么必须保留
git clone <remote> /tmp/remote-check
ls /tmp/remote-check/

# 2. 选择性 cp，不要 rsync --delete 或 git add .
# 明确写出要推的文件：
cp report.html sections/ data/ FULL_REPORT.md /tmp/remote-check/

# 3. dry-run 看 diff
cd /tmp/remote-check
git status --short
git diff --stat report.html  # 异常大的 diff 警觉

# 4. 提交（信息写"为什么"）
git commit -m "Fix HTML layout: missing </div> at L332 caused grid collapse in summary"
```

### 3.2 .gitignore 默认条目

```
# 工作产物
WORKING/
*_backup.*
*.DS_Store

# PPT 实验
*.pptx
generate_deck*.py
html_to_pptx.py
deck_outline.md
section_pngs/

# Python
__pycache__/
*.pyc
.venv/

# Playwright 截图临时目录
screenshots/
slide-*.jpg
slide-*.png
```

### 3.3 commit message 模板

```
<type>: <一句话总结，写"为什么"不是"什么">

- 具体变更 1（含定位：文件/行号）
- 具体变更 2
- 影响范围 / 验证方法

Co-Authored-By: Claude Opus 4.7 (1M context) <noreply@anthropic.com>
```

`<type>`：Fix / Add / Update / Refactor / Doc / Chore

---

## 4. 症状 → 根因排查（用户截图反馈时）

| 症状 | 根因 | 修复 |
|---|---|---|
| 文字单字换行 0./.2 | div / grid 容器破损 | div balance check |
| 整页空白 | section padding 错 / 100vh | grep `100vh\|padding-top` |
| 图表 Loading 不出来 | CDN 没加载 / 等待不够 | wait_for_selector("canvas") |
| TOC 链接跳不到 | anchor id 和 href 不匹配 | grep `id=` vs `href="#` |
| 字看不清 | 低对比度（深底深字） | 改 CSS variables |
| 文字溢出卡片 | overflow 没设 / 字号大 | `overflow: hidden` + 缩字 |
| 同字号视觉大小不一 | clamp / vw 单位 + 容器宽不同 | 改固定 px / rem |

**纪律**：用户发截图反馈时，先对照表查根因；猜错根因 = 二次破坏。

---

## 5. 完整 delivery checklist（v-final 前跑一遍）

- [ ] `report.html` div balance check 通过
- [ ] 所有 section 单独 balance check 通过
- [ ] Playwright 取核心 8-10 个 section 截图，肉眼无异常
- [ ] grep `style="margin` 应为 0（pitfall #10）
- [ ] grep `[UNSOURCED]` 数量 ≤ 5%
- [ ] 强词扫描：`必然 | 稳态 | 全链 | 世代`（pitfall #7）
- [ ] 数字一致性：TAM / CAGR / PSR / DCF 咬合（pitfall #12）
- [ ] 引语 attribution web-verify（pitfall #13）
- [ ] 仓库推送：实验产物已排除，远端入口文件未覆盖
- [ ] commit message 写清"为什么"
