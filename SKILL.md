---
name: industry-report
description: Generate PE-grade industry research reports for ANY industry (manufacturing, AI software, consumer, services, healthcare, energy, fintech, etc.). Adapts framework to the specific industry instead of forcing a fixed template. Use when user asks "研究 X 行业"、"做一份 Y 的研报"、"PE 视角分析 Z 产业"、"对标弘毅做一份 X 的研究".
allowed-tools: Task, WebSearch, WebFetch, Read, Write, Edit, Bash, TodoWrite
---

# Industry Report Generation Pipeline (Universal)

You are running a **5-phase universal industry research pipeline**. The most important rule: **NEVER fix the chapter structure before completing Phase 1 diagnosis**. Different industries have different essences—forcing one template is the #1 mistake.

---

## Phase 0 · Pre-flight (read before starting)

Read these in order:
1. `methodology/05_pitfalls.md` — **8 ironclad rules. Do not skip.**
2. `methodology/01_diagnose.md` — How to diagnose industry essence
3. `methodology/02_chapter_modules.md` — Module library (16 modules)
4. `methodology/03_information_sources.md` — Industry-specific source strategy
5. `methodology/04_pipeline.md` — 5-phase execution detail
6. `methodology/06_style_guide.md` — Writing conventions (mandatory)
7. `methodology/07_critic_protocol.md` — Adversarial review protocol

Then ask the user for:
- Industry / topic
- (Optional) Reference report to learn THINKING from (NOT to copy structure)
- (Optional) Specific angle of interest (PE / strategy / competitive / market entry)

Do NOT proceed until Phase 1 is complete.

---

## Phase 1 · Industry Diagnosis (mandatory, ~10 min)

Before any web search, answer:

1. **Industry archetype**: Manufacturing / Early-stage tech / AI software / Consumer / Services / Healthcare / Energy / Fintech / Other?
2. **Maturity**: Pre-PMF / Early growth / Growth / Mature / Decline?
3. **What is THE core tension / mattering thing in this industry?**
   - Manufacturing → supply chain, cost, scale, policy
   - Early tech → technology paths, PMF, player approaches, valuation
   - AI software → model capability, distribution, unit economics, data moat
   - Consumer → brand, channel, user insight, unit economics
   - Services → marketplace dynamics, network effects, unit economics
   - Healthcare → pipeline, clinical data, indication, payer, regulation
   - Energy → tech, scale, policy, economics, supply chain
   - Fintech → regulation, unit economics, risk model, network effects
4. **What would the SHARPEST analyst point to as "the question that matters"?**
5. **What chapter modules from the library best fit?** (See `methodology/02_chapter_modules.md`)

Write Phase 1 conclusion to `WORKING/phase1_diagnosis.md`. **The user reviews and confirms before Phase 2.**

---

## Phase 2 · Chapter Assembly (5-15 min, based on Phase 1)

From `modules/` directory, select **5-8 modules** for THIS industry. NOT a fixed 5.

**Always include (4 universal modules)**:
- `industry_essence.md` — Why now? Underlying drivers.
- `top_voices.md` — Real opinions of top founders / investors / scholars (public sources).
- `scenarios_catalysts.md` — Key variables + scenarios + 12-24 month catalyst calendar.
- `open_questions.md` — Unresolved debates that determine outcomes.

**Conditionally include (12 specialized modules)**: Pick what fits the industry diagnosis:
- `tech_routes.md` — When tech paths are contested (early tech, AI, biotech R&D)
- `business_model_routes.md` — When SaaS/PLG/MQL/RaaS/marketplace models compete
- `value_chain.md` — When physical supply chain matters (manufacturing, hardware)
- `player_paths.md` — When players take meaningfully different bets (almost always)
- `commercialization_validation.md` — DD-grade reality check on orders/autonomy/PMF
- `unit_economics.md` — LTV/CAC/payback/contribution margin (services, SaaS, consumer)
- `user_demand_insight.md` — Survey/interview/ethnography (consumer, B2C)
- `channel_distribution.md` — When channels are the moat (consumer, B2B sales)
- `policy_environment.md` — Subsidies / sanctions / tariffs (regulated, geopolitical)
- `regulatory_path.md` — FDA / SEC / approval bottleneck (healthcare, fintech)
- `geopolitics.md` — Cross-border, US-China, export controls
- `store_cohort_model.md` — Single-unit model (retail, restaurants, SaaS cohorts)

Write Phase 2 outline to `WORKING/phase2_outline.md`. User reviews before Phase 3.

---

## Phase 3 · Information Source Strategy (5 min)

Read `methodology/03_information_sources.md`. Build an industry-specific source plan:
- Which authoritative databases / reports?
- Which top voices to search? (Founders + investors + scholars + critics)
- Which media / podcasts / blogs?
- Which conferences / annual reports / earnings calls?
- Which regulator / industry association?

Write source plan to `WORKING/phase3_sources.md`.

---

## Phase 4 · Parallel Agent Execution (~25 min)

For each module from Phase 2, launch a `general-purpose` agent with a specific prompt derived from `templates/agent_prompt.md.j2`. Run **all in parallel** in a single message.

After parallel agents return: 1 round of self-review → identify gaps → launch supplement agent(s) (~10 min).

---

## Phase 5 · Mandatory Verification (~15 min parallel)

Launch **3 verification agents in parallel** (applies to ALL industries):
1. **top_voices verification** — Cross-check with real public quotes (using `methodology/07_critic_protocol.md`)
2. **DD metrics deep-dive** — Industry-specific (for hardware: MTBF; for SaaS: cohort retention; for consumer: same-store growth; for biotech: phase data)
3. **Adversarial critic** — Hunt fatal flaws, math errors, sourcing gaps, overconfident claims

Apply findings:
- **Fatal flaws** → fix inline (no separate ERRATA section in the final report; that's for internal tracking)
- **Severe issues** → fix
- **Suggestions** → consider; don't bloat

---

## Phase 6 · HTML Synthesis

Use `templates/html_skeleton.html` as base. Chart.js + Mermaid + Tailwind CSS via CDN.

**Critical**: PE deal-level tools (IC memo, decision tree, portfolio allocation, Q&A standard answers) belong in **appendix**, not the main report. Industry research and deal tools are different products.

---

## Phase 7 · References DB

Build `data/references.json` + `data/data_points.json` from agent outputs. Every key number traceable. Confidence labels: high / medium / low.

---

## Final Output Structure

```
<output_dir>/
├── FULL_REPORT.md            # Main report
├── report.html               # Visual report (single-file HTML)
├── sections/                 # Per-module deep markdown
├── data/                     # JSON refs / data points / companies
└── WORKING/                  # Phase 1-3 conclusions (kept for traceability)
```

---

## ⚠️ THE 8 IRONCLAD RULES (from methodology/05_pitfalls.md)

1. **No template forcing** — Phase 1 diagnosis is the only basis for chapter selection
2. **Industry essence > Framework** — Ask "what's the core matter?" before "what's the structure?"
3. **Information sources > Inference** — ALWAYS search real public statements from top voices; never rely on training memory
4. **PE deal tools belong in appendix** — IC memo, decision tree, portfolio allocation, Q&A → never in main body
5. **Every number traceable** — Mark `[UNSOURCED]` / `[INFERRED]` / `[UNDISCLOSED]` when uncertain
6. **Math twice** — Pricing formulas (× hours × days), revenue forecasts (vs TAM), DCF inputs—verify arithmetic
7. **Soften strong words** — 必然/稳态/全链垄断/世代级机会 → 大概率/当前格局/主导/历史级量级机会
8. **Always run adversarial critic** — v1 → critic → fix; ERRATA is internal note, NOT a chapter
