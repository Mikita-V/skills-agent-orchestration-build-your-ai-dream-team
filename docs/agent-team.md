# Agent team

Mona's Project Pulse dashboard will be built by a custom four-agent team, orchestrated through GitHub Copilot CLI in a Codespace. The Orchestrator coordinates the specialists, assigns non-overlapping file scopes, sequences dependent work, and confirms the integrated result.

| Agent | Target model | Responsibility | Definition |
|---|---|---|---|
| Orchestrator | Claude Opus 4.7 (copilot) | Coordinates the team from Copilot CLI, obtains the plan, turns it into dependency-aware phases, delegates explicit file scopes, and verifies the integrated dashboard. | `.github/agents/orchestrator.agent.md` |
| Planner | Claude Opus 4.7 (copilot) | Researches the repository and relevant documentation, identifies requirements, risks, dependencies, and edge cases, then produces an implementation plan with file ownership and validation expectations. | `.github/agents/planner.agent.md` |
| Designer | Gemini 3.1 Pro (copilot) | Owns UI/UX direction, accessibility, information hierarchy, interaction flow, responsive behavior, and Project Pulse's polished dashboard styling. | `.github/agents/designer.agent.md` |
| Coder | GPT-5.5 (copilot) | Implements assigned application logic and bug fixes with explicit errors and testable behavior; for Project Pulse, it can also create the assigned VS Code launch configuration for previewing the dashboard. | `.github/agents/coder.agent.md` |

All agents leave staging, commits, and pushes to the learner through Copilot CLI prompts.
