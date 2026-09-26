# GitHub Copilot Custom Instructions

## Hackathon Evaluation Skill

When asked to evaluate this codebase or when the `/hack-eval` command is triggered:
- Activate the skill defined in `.agents/skills/hack-eval/SKILL.md`.
- Evaluate across the 5 defined parameters totaling 450 marks.
- Maintain strict read-only execution: create only `hack_evaluation.md`.
- Commit `hack_evaluation.md` with: `chore: add AI agent hackathon evaluation`.
- Respond in chat with strictly `File created`.
