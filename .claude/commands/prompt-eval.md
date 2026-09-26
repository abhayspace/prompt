# Prompt Evaluation Command (`/prompt-eval`)

Execute the Prompt Evaluation skill (`prompt-eval`) to evaluate and grade any prompt.

## Arguments Provided:
$ARGUMENTS

## Instructions:
1. **Target Prompt:**
   - If `$ARGUMENTS` contains prompt text or a file path, evaluate that target.
   - If missing, prompt the user: "Please provide the prompt text or the path to the prompt file you would like to evaluate."
2. **Evaluation Protocol:**
   - Read `.agents/skills/prompt-eval/SKILL.md`.
   - Score the 3 criteria totaling **250 marks**:
     - Prompt Clarity (0-100)
     - Output Quality & Schema Compliance (0-100)
     - Efficiency & Token Economy (0-50)
   - Generate `prompt_eval.md` including score table, detailed analysis, and a production-ready optimized rewrite.
3. **Commit & Respond:**
   - Stage and commit `prompt_eval.md` with message: `chore: add prompt evaluation report`.
   - Provide score summary in chat and point to `prompt_eval.md`.
