---
description: Evaluate a prompt across Prompt Clarity (100), Output Quality (100), and Efficiency (50) - 250 marks total
---

# /prompt-eval

Evaluate the provided prompt or target prompt file against prompt engineering standards.

## Instructions
1. Inspect the prompt text provided in the prompt argument or specified file path. If missing, ask the user to provide the prompt text or file path.
2. Follow all guidelines in `.agents/skills/prompt-eval/SKILL.md`.
3. Score the 3 parameters:
   - Prompt Clarity (0-100)
   - Output Quality (0-100)
   - Efficiency (0-50)
   - Total Score: 250 marks
4. Generate `prompt_eval.md` at project root including score table, analysis, and an optimized prompt rewrite.
5. Commit `prompt_eval.md` with: `chore: add prompt evaluation report`.
6. Output a brief summary in chat.
