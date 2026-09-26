# OpenCode Command: /prompt-eval

When `/prompt-eval [prompt_or_file]` is executed:

1. **Target Identification:**
   - Use the prompt text or file path passed with the command.
   - If missing, prompt user: "Please provide the prompt text or the path to the prompt file you would like to evaluate."
2. **Execute Evaluation:**
   - Follow instructions in `.agents/skills/prompt-eval/SKILL.md`.
   - Score the 3 parameters: Prompt Clarity (/100), Output Quality (/100), Efficiency (/50) totaling **250 marks**.
   - Create `prompt_eval.md` with scoring, findings, and an optimized rewrite.
3. **Commit & Reply:**
   - Commit `prompt_eval.md` with message `chore: add prompt evaluation report`.
   - Output summary in chat.
