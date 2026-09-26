# OpenCode Command: /hack-eval

When `/hack-eval [problem_statement]` is executed:

1. **Problem Statement Resolution:**
   - Use the problem statement passed with the command if available.
   - Otherwise, check `.agents/skills/hack-eval/SKILL.md`.
   - If missing, pause and prompt the user:
     "Please provide the hackathon problem statement to begin the AI agent evaluation."
2. **Execute Evaluation Skill:**
   - Follow instructions in `.agents/skills/hack-eval/SKILL.md`.
   - Conduct a read-only audit of the harness.
   - Score the 5 parameters totaling **450 marks**.
   - Create `hack_evaluation.md`.
3. **Commit & Reply:**
   - Commit `hack_evaluation.md` with message `chore: add AI agent hackathon evaluation`.
   - Reply in chat with strictly `File created`.
