# Project Pulse Implementation Plan

## Goal

Build a static Project Pulse dashboard that loads realistic project data from JSON and presents multiple project cards in an accessible, responsive interface. Meet the requirements in `.github/project-pulse-brief.md`, `.github/steps/3-step.md`, and `.github/workflows/3-step.yml`, while following the ownership conventions in `docs/agent-team.md` and `.github/agents`.

## Roles and File Assignments

| Role | Responsibility | Files |
| --- | --- | --- |
| Designer | Provide a UI handoff only; define responsive hierarchy, semantic and accessibility guidance, contrast, badge labels, spacing, mobile behavior, and loading, empty, and error states. | No edits |
| Coder | Create data and preview configuration, then implement and integrate the dashboard. | `app/index.html`, `app/styles.css`, `app/project-data.json`, `.vscode/launch.json` |
| Orchestrator | Sequence dependent work and verify the integrated result. | No implementation edits |

## Phases and Dependencies

1. Gather the Designer handoff and confirm the JSON schema: `project-data.json` has a top-level `projects` array with multiple realistic records containing `name`, `owner`, `status`, `recentActivity`, and `priority`.
2. Coder creates `app/project-data.json` and `.vscode/launch.json`. The launch file must be comment-free, strict JSON, with a `Run Project Pulse Dashboard` configuration running `python3 -m http.server 5500` from `${workspaceFolder}/app`; `serverReadyAction` must open `http://localhost:%s/index.html`.
3. After the handoff and schema are available, Coder implements `app/index.html` and `app/styles.css` together. The page must use the exact title `Project Pulse`, semantic structure, link the stylesheet, fetch `project-data.json`, render a `.project-card` per project, show owner/status/recentActivity/priority and a contributor summary, and handle loading, empty, error, and unknown status/priority fallback states.
4. Integrate after all artifacts exist. The HTML links the CSS and data; the launch configuration is independent to author but requires `index.html` for runtime preview. Final validation depends on all targets.

## Parallel Work Decisions

The Designer handoff, JSON data, and launch configuration can proceed in parallel because they do not edit or depend on each other. HTML and CSS must follow the approved handoff and data schema, so they are coordinated sequentially after those inputs. Integration is last to catch cross-file loading and rendering failures.

## Validation Expectations

- Run `python3 -m json.tool` on `app/project-data.json` and `.vscode/launch.json`.
- Run `bash scripts/validate-exercise.sh` once all required artifacts exist.
- Check the source against the stated requirements, including the exact title, JSON fetch, per-project cards, and state/fallback handling.
- Preview the launch configuration on port `5500`; confirm it opens `index.html` rather than a directory listing and shows multiple project cards.
- Review desktop and mobile layouts for semantic accessibility, contrast, keyboard focus visibility, overflow, long-content wrapping, and responsive grid behavior.

## Scope/Edge Cases

- Keep all implementation ownership with Coder; Designer supplies direction only and does not edit files.
- Style `.dashboard`, `.project-card`, status and priority badges, a responsive grid, border radius, and box shadow.
- Ensure small screens and long names/activity text wrap or scroll appropriately without overlap.
- Render safe unknown labels or neutral styling for unrecognized status and priority values rather than failing.
- Make loading, empty data, and fetch-error states legible and accessible.