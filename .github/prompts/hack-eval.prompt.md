---
description: Run an AI Agent Hackathon Evaluation across 5 parameters (450 marks total)
---

# /hack-eval

Evaluate this AI agent repository against the hackathon problem statement.

## Instructions
1. Check if the user passed a problem statement in this prompt or if it is configured in `.agents/skills/hack-eval/SKILL.md`. If missing, ask the user to provide it.
2. Follow all guidelines in `.agents/skills/hack-eval/SKILL.md`.
3. Perform a comprehensive read-only review of the entire agent harness.
4. Score all 5 parameters:
   - Problem Statement Alignment (0-100)
   - Code Quality (0-100)
   - Innovation (0-100)
   - Security (0-100)
   - Grounding and Evals (0-50: Grounding 25, Evals 25)
   - Total Score: 450 marks
5. Generate the complete judging report in `hack_evaluation.md`.
6. Stage only `hack_evaluation.md` and commit with message: `chore: add AI agent hackathon evaluation`.
7. Respond in chat with strictly:
   `File created`
