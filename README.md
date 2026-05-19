# industry-report-skill

> A Claude Code Skill that generates **PE-grade industry research reports for ANY industry**, adapting the framework to the specific industry instead of forcing a fixed template.

---

## What this skill does

Input: an industry / topic (e.g., "具身智能", "AI 编程工具", "固态电池", "新茶饮", "创新药 PD-1")

Output:
- `FULL_REPORT.md` — main markdown
- `report.html` — single-file HTML with Chart.js / Mermaid / Tailwind (~250 KB)
- `sections/*.md` — per-module deep markdown
- `data/references.json` + `data_points.json` + `companies.json` — traceable references DB

Pipeline: **5 phases** taking ~2-3 hours, parallel agents, with mandatory adversarial review.

**Key principle**: NEVER forces a fixed chapter structure. **Phase 1 diagnoses the industry first**, then assembles 5-8 chapters from a 16-module library based on what actually matters for THIS industry.

---

## Why this is different from "just prompting Claude"

Most industry reports built with LLMs fail because they:
1. Copy template structure from a reference industry that doesn't fit (e.g., forcing battery supply-chain structure onto AI software)
2. Rely on training memory (which is stale and unverified)
3. Mix industry research with PE deal-level tools (IC memos, decision trees) in the main body
4. Use vague strong claims ("certainly", "absolute moat") without falsifiable conditions
5. Get basic math wrong (pricing formulas, TAM ratios, DCF inputs)
6. Skip adversarial review

This skill encodes **8 ironclad rules** (see `methodology/05_pitfalls.md`) born from a real PE-grade research project's hard lessons.

---

## Installation

### On a new machine

```bash
# Clone the skill into ~/.claude/skills/ (note: target dir must be "industry-report",
# matching the `name:` field in SKILL.md, NOT the repo name "industry-report-skill")
git clone https://github.com/xiongjjlj/industry-report-skill.git ~/.claude/skills/industry-report
```

That's it. Claude Code automatically picks up skills in `~/.claude/skills/` at startup.

### On a machine where you develop the skill (e.g. this Mac)

Keep working copy under `~/Downloads/...` for easy git push/pull, and symlink it into the skills dir so Claude Code can see it:

```bash
ln -s /path/to/your/working/industry-report-skill ~/.claude/skills/industry-report
```

This way: edit in `~/Downloads/`, `git commit && git push`, no `cp` needed — Claude Code reads through the symlink.

### Verify install

In Claude Code:
```
> /list-skills
```
You should see `industry-report` listed.

---

## Usage

### Basic

```
> 用 industry-report skill 帮我研究 {INDUSTRY}
```

或：

```
> 帮我做一份 {INDUSTRY} 的 PE 视角行业研究报告
> 对标弘毅资本《全球电池与电动车产业链格局分析》的专业度
```

Claude will then:
1. **Phase 1**: Diagnose the industry (asks you to confirm before proceeding)
2. **Phase 2**: Propose 5-8 chapter modules from the library (asks you to confirm)
3. **Phase 3**: Build information source strategy
4. **Phase 4**: Launch N parallel agents (one per module)
5. **Phase 5**: 3 verification agents in parallel (top voices + DD metrics + adversarial critic)
6. **Phase 6**: Synthesize HTML report
7. **Phase 7**: Build references DB

### Custom output directory

```
> 用 industry-report 研究 AI 编程工具，输出到 ~/Reports/ai-coding-2026/
```

### Reference report mode

If you have a reference report you want to learn THINKING from (not copy structure):

```
> 用 industry-report 研究 {INDUSTRY}；参考 {reference_pdf_path} 的分析思维
```

The skill will extract the THINKING from the reference (e.g., "for battery industry, supply chain matters because cost/scale/policy are the core tensions") and apply it diagnostically (e.g., "for AI software, supply chain is irrelevant; model capability + distribution + unit economics are the core tensions").

---

## Repository structure

```
industry-report-skill/
├── SKILL.md                          # Main skill entry (Claude reads first)
├── README.md                         # This file
├── methodology/                      # ⭐ The "know-how" — read all 7
│   ├── 01_diagnose.md                # How to diagnose industry essence
│   ├── 02_chapter_modules.md         # 16-module library + archetype combos
│   ├── 03_information_sources.md     # Source strategy by archetype
│   ├── 04_pipeline.md                # 5-phase orchestration
│   ├── 05_pitfalls.md                # ⚠️ 8 ironclad rules
│   ├── 06_style_guide.md             # Writing conventions
│   └── 07_critic_protocol.md         # Adversarial review protocol
├── modules/                          # 16 chapter prompt templates
│   ├── industry_essence.md           # Always
│   ├── top_voices.md                 # Always
│   ├── scenarios_catalysts.md        # Always
│   ├── open_questions.md             # Always
│   ├── tech_routes.md                # Conditional
│   ├── business_model_routes.md      # Conditional
│   ├── value_chain.md                # Conditional
│   ├── player_paths.md               # Conditional
│   ├── commercialization_validation.md  # Conditional
│   ├── unit_economics.md             # Conditional
│   ├── user_demand_insight.md        # Conditional
│   ├── channel_distribution.md       # Conditional
│   ├── policy_environment.md         # Conditional
│   ├── regulatory_path.md            # Conditional
│   ├── geopolitics.md                # Conditional
│   └── store_cohort_model.md         # Conditional
├── templates/                        # Rendering templates
│   ├── html_skeleton.html            # HTML skeleton (Chart.js + Mermaid + Tailwind)
│   └── agent_prompt.md.j2            # Per-module agent prompt template
└── examples/                         # Gold-standard reference reports
    └── embodied_ai_2026/              # ⭐ Real PE report this skill was distilled from
        ├── report.html
        ├── FULL_REPORT.md
        ├── sections/
        └── data/
```

---

## The 8 ironclad rules (read `methodology/05_pitfalls.md` for full)

1. **No template forcing** — Phase 1 diagnosis is the only basis for chapter selection
2. **Industry essence > Framework** — Ask "what's the core matter?" before "what's the structure?"
3. **Information sources > Inference** — ALWAYS search real public statements from top voices; never rely on training memory
4. **PE deal tools belong in appendix** — IC memo, decision tree, portfolio allocation, Q&A → never in main body
5. **Every number traceable** — Mark `[UNSOURCED]` / `[INFERRED]` / `[UNDISCLOSED]` when uncertain
6. **Math twice** — Pricing formulas, revenue forecasts vs TAM, DCF inputs—verify arithmetic
7. **Soften strong words** — 必然/稳态/全链垄断/世代级机会 → 大概率/当前格局/主导/历史级量级机会
8. **Always run adversarial critic** — v1 → critic → fix; ERRATA is internal note, NOT a chapter

---

## Archetype-specific chapter recommendations

| Industry archetype | Recommended modules (typical 7-9 chapters) |
|---|---|
| **Early-stage tech** (具身智能 / 脑机接口 / 量子) | essence + voices + tech_routes + player_paths + commercialization_validation + value_chain + scenarios + open_questions |
| **AI software** (LLM / 编程 / Vertical AI) | essence + voices + tech_routes + business_model_routes + unit_economics + player_paths + commercialization_validation + scenarios + open_questions |
| **Manufacturing** (储能 / 光伏 / 半导体) | essence + voices + value_chain + player_paths + policy_environment + geopolitics + scenarios + open_questions |
| **Consumer** (新茶饮 / SHEIN / POP MART) | essence + voices + user_demand_insight + channel_distribution + store_cohort_model + player_paths + unit_economics + scenarios + open_questions |
| **Healthcare R&D** (创新药 / 医疗器械) | essence + voices + tech_routes + regulatory_path + player_paths + commercialization_validation + scenarios + open_questions |
| **Fintech** (稳定币 / 跨境支付) | essence + voices + regulatory_path + business_model_routes + unit_economics + player_paths + geopolitics + scenarios + open_questions |
| **Energy** (储能 / 氢能) | essence + voices + value_chain + tech_routes + policy_environment + unit_economics + scenarios + open_questions |
| **Service platforms** (滴滴 / 美团) | essence + voices + business_model_routes + unit_economics + player_paths + regulatory_path + scenarios + open_questions |

---

## Example: embodied_ai_2026 reference report

This skill was distilled from a real PE research project on humanoid robotics / embodied AI.

The final report is in `examples/embodied_ai_2026/`:
- 277 KB single-file HTML
- 6 markdown deep sections (~60,000 字 / 60+ figures)
- 206 references / 210 data points / 81 company profiles
- Generated with: 5 parallel research agents + adversarial critic + verification

See `examples/embodied_ai_2026/report.html` to know what the output looks like.

---

## What's NOT in this skill

- **Real-time data**: All numbers come from public sources via WebSearch; this skill doesn't have Bloomberg / PitchBook / IT 桔子 API access. If you have these, you can configure them as MCP servers (out of scope here).
- **First-hand interviews**: Use lark-mail / Slack to outreach. This skill is for desk research.
- **Excel financial models**: Add a separate `anthropic-skills:xlsx` call after the report is generated.
- **PPT generation**: Add a separate `anthropic-skills:pptx` call to convert the HTML report to slides.

---

## Cost estimate

A full report typically uses:
- 5-8 parallel research agents × ~50K tokens each
- 3 verification agents × ~50K tokens each
- Synthesis + HTML rendering ~30K tokens
- **Total ~500K-800K tokens** (mostly Sonnet-tier agents)
- **Wall time ~2-3 hours** (parallel)

---

## Customization

### Add new modules

Drop a new markdown file in `modules/`, list its core questions / expected output / pitfalls (follow existing format), and add it to `methodology/02_chapter_modules.md`.

### Change style

Edit `methodology/06_style_guide.md`. Style applies to all reports.

### Different output language

By default Chinese (中文). For English reports, modify `templates/agent_prompt.md.j2` and `templates/html_skeleton.html` strings.

---

## License

MIT. Fork freely.

---

## Built by

Distilled from a real PE-grade research project. Built iteratively over multiple rounds of harsh feedback. The 8 ironclad rules are battle-scars, not theory.
