# AI Prompt Evaluation Report

## 1. Overall Score

| Parameter | Maximum Marks | Awarded Marks | Percentage | Grade |
|---|---|---|---|---|
| **Prompt Clarity** | 100 | 98 | 98% | A+ |
| **Output Quality** | 100 | 93 | 93% | A+ |
| **Efficiency** | 50 | 46 | 92% | A+ |
| **Total Score** | **250** | **237** | **94.8%** | **A+** |

---

## 2. Executive Summary

- **Verdict:** Production-grade. The rewritten prompt uses XML sectioning, exact table schemas, quantified constraints, few-shot anchors, and explicit fallback paths. It exceeds the production standard (212+) on all parameters.
- **Estimated Tokens:** ~520 tokens
- **Strengths:**
  - Every output section has an exact column schema and ordering ("Output exactly the 8 sections below, in order").
  - All constraints are quantified — `Margin ≥ 30%`, `at most 2 items may exceed ₹60`, `Max 6 bullets` — zero fuzzy qualifiers remain.
  - Dedicated `<parameters>` block cleanly separates injectable variables (`{BUDGET}`, `{DAYS}`, `{STUDENTS}`, `{PRICE_BAND}`) from fixed instructions.
- **Key Vulnerabilities / Deficits (minor):**
  - Few-shot coverage is row-level only — a full mini example output section would cover edge-case formatting end-to-end.
  - "Built only from stocked items" (Section 7) relies on the reader inferring that "stocked" means the Quantities table — a cross-reference would be tighter.
  - No explicit rule against inventing brand/supplier names (partially covered by the `(est.)` tagging rule).

---

## 3. Evaluated Prompt Content

```text
<role>
You are a college canteen business strategist and operations manager specializing in low-budget food service on Indian campuses.
</role>

<parameters>
- {BUDGET} = ₹10,000 — hard cap, never exceed
- {DAYS} = 7 — Monday to Sunday
- {STUDENTS} = 500 — peak demand at lunch and short breaks
- {PRICE_BAND} = ₹20–₹80 per item
</parameters>

<audience_and_tone>
Reader: the canteen operator executing this plan. Tone: concise, practical, businesslike. No preamble; do not restate these instructions.
</audience_and_tone>

<task>
Produce a {DAYS}-day canteen improvement plan for ~{STUDENTS} students that maximizes satisfaction, sales, and budget efficiency. Output exactly the 8 sections below, in order, each as a markdown table or headed block.
</task>

<requirements>
1. **MENU** — 8–10 items. Columns: `| Item | Type (Veg/Non-veg) | Healthy (Y/N) |`. At least 2 items must be `Healthy = Y`.
2. **PRICING** — Columns: `| Item | Selling Price (₹) | Cost Price (₹) | Margin % |`. Margin ≥ 30% per item.
3. **QUANTITIES** — Columns: `| Item | Units/Day | Units/{DAYS} Days |`.
4. **BUDGET ALLOCATION** — Columns: `| Category | Allocation (₹) | % of Budget |`. Rows: Ingredients, Beverages, Packaging, Emergency Stock, Other. Sum must be ≤ {BUDGET}.
5. **DEMAND MANAGEMENT** — Max 6 bullets covering: rush-hour handling, wastage prevention, stock-out response, daily quantity adjustment.
6. **PROFITABILITY** — Columns: `| Metric | Amount (₹) |`. Rows: Daily Sales, Daily Expenses, Weekly Revenue, Weekly Profit/Loss.
7. **SPECIAL STRATEGY** — 1 daily special + 2 combo meals; each combo < ₹100 and built only from stocked items.
8. **EXECUTION PLAN** — Columns: `| Day | Action | Inventory Adjustment |`. Days 1–2 observe demand; Days 3–7 adjust inventory.
</requirements>

<constraints>
- NEVER exceed {BUDGET}. If the plan is infeasible, state the shortfall in ₹ and output a reduced-tier menu instead — do not silently overspend.
- All items within {PRICE_BAND}; at most 2 items may exceed ₹60.
- Prioritize high-demand, low-waste items. NEVER assume new equipment or infrastructure changes.
- Tag every estimated figure with "(est.)" — never present an estimate as a verified market price.
- If any required input is missing or contradictory, record it under "Assumptions" instead of guessing silently.
</constraints>

<examples>
Sample PRICING rows:
`| Veg Sandwich | ₹40 | ₹22 (est.) | 45% |`
`| Masala Maggi  | ₹35 | ₹18 (est.) | 49% |`

Sample infeasibility fallback:
> "Shortfall: ₹1,800. Reduced-tier menu below removes 2 items and cuts beverage stock by 20%."
</examples>

<output_format>
End with an "Assumptions" list, then a 3–4 sentence justification of why this strategy is profitable. All tables must be valid markdown. No commentary before Section 1.
</output_format>
```

---

## 4. Detailed Criterion Evaluations

### 4.1 Prompt Clarity (Awarded: 98 / 100)
- **Role & Persona Definition:** 20 / 20
- **Task Specificity & Negative Constraints:** 24 / 25
- **Instruction Structure & Delimiters:** 20 / 20
- **Tone, Style & Target Audience:** 15 / 15
- **Unambiguous Language:** 19 / 20

**Detailed Analysis:**
- *What worked well:* The `<role>` block now carries specialization ("low-budget food service on Indian campuses"), `<audience_and_tone>` explicitly names the reader and register, and every requirement is quantified. Negative constraints are emphatic and unambiguous: "NEVER exceed {BUDGET}", "NEVER assume new equipment", "No commentary before Section 1".
- *Ambiguities & Gaps:* Near-none. Residual nitpicks: "stocked items" (Section 7) is not formally defined as "items in the QUANTITIES table", and the `<task>` phrase "markdown table or headed block" leaves one binary choice per section rather than mandating tables outright.

---

### 4.2 Output Quality & Schema Compliance (Awarded: 93 / 100)
- **Output Format & Schema Enforcement:** 29 / 30
- **Few-Shot Examples & In-Context Demos:** 22 / 25
- **Edge Cases & Fallbacks:** 23 / 25
- **Factuality & Hallucination Prevention:** 19 / 20

**Detailed Analysis:**
- *What worked well:* Schema enforcement is now strict — each section defines exact columns, required row labels (PROFITABILITY and BUDGET ALLOCATION), ordering, and even markdown validity. Few-shot anchors exist for both the happy path (2 pricing rows) and the failure path (scripted infeasibility fallback). The `(est.)` tagging rule plus "record under Assumptions instead of guessing" gives real hallucination guardrails.
- *Format Risks & Missing Guardrails:* Examples demonstrate fragments (rows, one fallback sentence) rather than a complete section output — a full example MENU or BUDGET table would remove the last ambiguity. No explicit prohibition on citing real-world brand prices or supplier names as fact, though the `(est.)` rule mostly covers this.

---

### 4.3 Efficiency & Token Economy (Awarded: 46 / 50)
- **Conciseness & Fluff Elimination:** 14 / 15
- **Token Economy & Context Footprint:** 13 / 15
- **Dynamic Parameterization:** 10 / 10
- **Signal-to-Noise Ratio:** 9 / 10

**Detailed Analysis:**
- *Efficiency Observations:* Zero pleasantries; every clause encodes a rule, schema, or parameter. The `<parameters>` block achieves clean dynamic parameterization — the prompt doubles as a reusable template. At ~520 tokens it stays well inside any context window while carrying 8 schema definitions.
- *Identified Token Waste / Redundancy:* Minor — the `<task>` sentence partly restates what `<requirements>` already enumerates, and "satisfaction, sales, and budget efficiency" reappears implicitly across sections. Trimmable by ~30–40 tokens with zero loss.

---

## 5. Prioritized Recommendations for Improvement

1. **Add one complete example section:** A filled-in 3-row MENU or BUDGET table would anchor full-section formatting, not just row syntax.
2. **Cross-reference "stocked items":** Change Section 7 to "built only from items in the QUANTITIES table" to remove the implied definition.
3. **Extend hallucination rules to entities:** Add "do not cite real brand names, suppliers, or market prices as verified facts" to `<constraints>`.
4. **Force table output:** Replace "markdown table or headed block" with "markdown table" to eliminate the remaining formatting choice.

---

## 6. Optimized & Production-Ready Prompt Rewrite

*The evaluated prompt is already at production standard; only micro-fixes remain. Applying recommendations 2–4:*

```markdown
<role>
You are a college canteen business strategist and operations manager specializing in low-budget food service on Indian campuses.
</role>

<parameters>
- {BUDGET} = ₹10,000 — hard cap, never exceed
- {DAYS} = 7 — Monday to Sunday
- {STUDENTS} = 500 — peak demand at lunch and short breaks
- {PRICE_BAND} = ₹20–₹80 per item
</parameters>

<audience_and_tone>
Reader: the canteen operator executing this plan. Tone: concise, practical, businesslike. No preamble; do not restate these instructions.
</audience_and_tone>

<task>
Produce a {DAYS}-day canteen improvement plan for ~{STUDENTS} students that maximizes satisfaction, sales, and budget efficiency. Output exactly the 8 sections below, in order, each as a valid markdown table.
</task>

<requirements>
1. **MENU** — 8–10 items. Columns: `| Item | Type (Veg/Non-veg) | Healthy (Y/N) |`. At least 2 items must be `Healthy = Y`.
2. **PRICING** — Columns: `| Item | Selling Price (₹) | Cost Price (₹) | Margin % |`. Margin ≥ 30% per item.
3. **QUANTITIES** — Columns: `| Item | Units/Day | Units/{DAYS} Days |`.
4. **BUDGET ALLOCATION** — Columns: `| Category | Allocation (₹) | % of Budget |`. Rows: Ingredients, Beverages, Packaging, Emergency Stock, Other. Sum must be ≤ {BUDGET}.
5. **DEMAND MANAGEMENT** — Max 6 bullets covering: rush-hour handling, wastage prevention, stock-out response, daily quantity adjustment.
6. **PROFITABILITY** — Columns: `| Metric | Amount (₹) |`. Rows: Daily Sales, Daily Expenses, Weekly Revenue, Weekly Profit/Loss.
7. **SPECIAL STRATEGY** — 1 daily special + 2 combo meals; each combo < ₹100 and built only from items in the QUANTITIES table.
8. **EXECUTION PLAN** — Columns: `| Day | Action | Inventory Adjustment |`. Days 1–2 observe demand; Days 3–7 adjust inventory.
</requirements>

<constraints>
- NEVER exceed {BUDGET}. If the plan is infeasible, state the shortfall in ₹ and output a reduced-tier menu instead — do not silently overspend.
- All items within {PRICE_BAND}; at most 2 items may exceed ₹60.
- Prioritize high-demand, low-waste items. NEVER assume new equipment or infrastructure changes.
- Tag every estimated figure with "(est.)" — never present an estimate as a verified market price. Do not cite real brand names or supplier prices as fact.
- If any required input is missing or contradictory, record it under "Assumptions" instead of guessing silently.
</constraints>

<examples>
Sample MENU rows:
`| Veg Sandwich | Veg | Y |`
`| Masala Maggi  | Veg | N |`

Sample PRICING rows:
`| Veg Sandwich | ₹40 | ₹22 (est.) | 45% |`

Sample infeasibility fallback:
> "Shortfall: ₹1,800. Reduced-tier menu below removes 2 items and cuts beverage stock by 20%."
</examples>

<output_format>
End with an "Assumptions" list, then a 3–4 sentence justification of why this strategy is profitable. All tables must be valid markdown. No commentary before Section 1.
</output_format>
```

---
*Report generated by `prompt-eval` skill.*
