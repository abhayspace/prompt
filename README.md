# AI Evaluation Skills Repository

A suite of reusable evaluation skills designed for coding agents to rigorously judge hackathon submissions, AI agent harnesses, and prompt engineering implementations.

---

## ⚡ Quick Setup: Add These Skills to Any Project

To evaluate any hackathon submission or prompt using your preferred coding agent, copy the skill configuration into the root of the project you want to judge:

### 1. Copy Skill Configuration to Target Repository

**PowerShell (Windows):**
```powershell
# From the target project root, copy the skill files:
Copy-Item -Recurse -Force "path\to\eval_skill\.agents", "path\to\eval_skill\.claude", "path\to\eval_skill\.github", "path\to\eval_skill\.opencode", "path\to\eval_skill\AGENTS.md" -Destination .
```

**Bash / Terminal (macOS / Linux):**
```bash
# From the target project root, copy the skill files:
cp -r path/to/eval_skill/{.agents,.claude,.github,.opencode,AGENTS.md} .
```

*(Minimal universal setup: simply copy the `.agents/` folder and `AGENTS.md` file.)*

---

### 2. Available Skills & Slash Commands

| Skill | Slash Command | Criteria & Total | Output Report | Target |
|---|---|---|---|---|
| **Hackathon Agent Evaluator** | `/hack-eval` | Alignment (100) + Code Quality (100) + Innovation (100) + Security (100) + Grounding & Evals (50) = **450 Marks** | `hack_evaluation.md` | Full agent harness & codebase |
| **Prompt Evaluator** | `/prompt-eval` | Prompt Clarity (100) + Output Quality (100) + Efficiency (50) = **250 Marks** | `prompt_eval.md` | Any prompt text or prompt file |

---

### 3. Run Evaluations in Your Coding Agent

Open the target project in your coding assistant and run:

| Coding Agent | Hackathon Evaluation | Prompt Evaluation |
|---|---|---|
| **Antigravity (AGY)** | `/hack-eval` | `/prompt-eval <prompt_or_file>` |
| **Claude Code** | `/hack-eval` | `/prompt-eval <prompt_or_file>` |
| **GitHub Copilot** | Select `/hack-eval` | Select `/prompt-eval` |
| **OpenCode** | `/hack-eval` | `/prompt-eval <prompt_or_file>` |
| **Cursor / Others** | *"Execute /hack-eval"* | *"Execute /prompt-eval on [target]"* |

---

## Directory Structure

```text
eval_skill/
├── .agents/
│   ├── rules/
│   │   ├── hack-eval-command.md                  # Antigravity /hack-eval rule
│   │   └── prompt-eval-command.md                # Antigravity /prompt-eval rule
│   ├── skills.json                               # Skills configuration manifest
│   └── skills/
│       ├── hack-eval/                            # Hackathon Agent Evaluator Skill
│       │   ├── SKILL.md                          # Master executable evaluation skill
│       │   ├── references/
│       │   │   ├── scoring-rubric.md             # Scoring bands across 5 parameters
│       │   │   ├── security-checklist.md         # 5-dimension security audit checklist
│       │   │   └── harness-inspection-guide.md   # Step-by-step harness discovery guide
│       │   └── resources/
│       │       └── report-template.md            # Template for hack_evaluation.md
│       └── prompt-eval/                          # Prompt Evaluator Skill
│           ├── SKILL.md                          # Master prompt evaluation skill
│           ├── references/
│           │   └── scoring-rubric.md             # Scoring rubric across 3 criteria
│           └── resources/
│               └── report-template.md            # Template for prompt_eval.md
├── .claude/
│   └── commands/
│       ├── hack-eval.md                          # Claude Code /hack-eval command
│       └── prompt-eval.md                        # Claude Code /prompt-eval command
├── .github/
│   ├── copilot-instructions.md                   # GitHub Copilot agent instructions
│   └── prompts/
│       ├── hack-eval.prompt.md                   # GitHub Copilot /hack-eval prompt
│       └── prompt-eval.prompt.md                 # GitHub Copilot /prompt-eval prompt
├── .opencode/
│   └── commands/
│       ├── hack-eval.md                          # OpenCode /hack-eval command
│       └── prompt-eval.md                        # OpenCode /prompt-eval command
├── AGENTS.md                                     # Universal agent configuration
├── skills/
│   ├── hack-eval/                                # Mirrored hack-eval package
│   └── prompt-eval/                              # Mirrored prompt-eval package
└── README.md                                     # Repository documentation
```

---

## Skill 1: `hack-eval` (AI Agent Hackathon Evaluator)

Evaluates an AI agent harness across 5 parameters totaling **450 marks**:

| Parameter | Maximum Marks | Description |
|---|---|---|
| **1. Problem Statement Alignment** | 100 | Functional completeness, core use cases, edge case handling, output schema compliance. |
| **2. Code Quality** | 100 | Clean architecture, modularity, type safety, error handling, 12-factor config, tests, observability. |
| **3. Innovation** | 100 | Non-trivial agent architecture, orchestration (LangGraph, custom DAG), tools, memory, RAG innovations. |
| **4. Security** | 100 | Prompt injection defense, tool permissions/sandboxing, secret hygiene, RAG security, DoS/loop limits. |
| **5. Grounding and Evals** | 50 | **Grounding (25 pts):** Factual fidelity, citations, hallucination guards. <br>**Evals (25 pts):** Deterministic tests, trajectory evals, benchmark datasets. |
| **Total Score** | **450** | Total sum of all parameters. |

- Pre-configured with the **AI Travel Agent** hackathon challenge.
- Read-only execution: modifies **ONLY** `hack_evaluation.md`.
- Automatically commits: `chore: add AI agent hackathon evaluation`.
- Chat response: `File created`.

---

## Skill 2: `prompt-eval` (Prompt Evaluator)

Evaluates any written prompt, system prompt, or prompt template across 3 parameters totaling **250 marks**:

| Parameter | Maximum Marks | Description |
|---|---|---|
| **1. Prompt Clarity** | 100 | Role/persona definition (20), task specificity & negative constraints (25), delimiters/structure (20), tone & audience (15), unambiguous phrasing (20). |
| **2. Output Quality** | 100 | Output format & schema constraints (30), few-shot examples (25), edge case & fallback guidance (25), factuality & hallucination mitigation (20). |
| **3. Efficiency** | 50 | Conciseness & fluff elimination (15), token footprint & context economy (15), dynamic parameterization (10), signal-to-noise ratio (10). |
| **Total Score** | **250** | Total sum of all three parameters. |

- Output artifact: `prompt_eval.md`.
- Includes an **optimized, production-ready refactored version** of the evaluated prompt.
- Automatically commits: `chore: add prompt evaluation report`.
- Usage example:
  ```text
  /prompt-eval "You are an expert travel agent. Plan a 5-day trip to Tokyo."
  ```
  or evaluate a file:
  ```text
  /prompt-eval path/to/prompt.txt
  ```
