# Hackathon Agent Evaluation Command (`/hack-eval`)

Execute the AI Agent Hackathon Evaluator skill against this codebase.

## Arguments Provided:
$ARGUMENTS

## Instructions:
1. **Determine Problem Statement:**
   - If `$ARGUMENTS` contains a problem statement, use it as the authoritative ground truth.
   - If `$ARGUMENTS` is empty, check if `.agents/skills/hack-eval/SKILL.md` (or `skills/hack-eval/SKILL.md`) has a configured problem statement.
   - If missing, pause and ask the user in chat:
     "Please provide the hackathon problem statement to begin the AI agent evaluation."
2. **Execute Evaluation:**
   - Read `.agents/skills/hack-eval/SKILL.md`.
   - Inspect the codebase across all harness dimensions (architecture, tools, prompts, RAG, security, evals).
   - Score the 5 parameters totaling **450 marks** (Alignment 100, Code Quality 100, Innovation 100, Security 100, Grounding & Evals 50).
   - Generate `hack_evaluation.md` at the project root following the required report template.
   - Maintain strict read-only behavior: do NOT modify source code, configuration, or dependencies.
3. **Commit & Respond:**
   - Stage ONLY `hack_evaluation.md` (`git add hack_evaluation.md`).
   - Commit with message: `chore: add AI agent hackathon evaluation`.
   - Respond in chat with strictly:
     `File created`
