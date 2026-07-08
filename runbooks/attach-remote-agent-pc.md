# Runbook — Attach An Agent On Another PC

Recommended model: each PC runs its own local bridge for its local agent session.

## Requirements

- Codex/Claude installed and logged in on that PC
- project workspace available locally if source inspection is needed
- Hermes or a lightweight bridge runner installed
- Notion integration token available locally
- same message policy as `D:\AI_Hermes\memory\message-policy.md`

## Steps

1. Open or clone the project workspace on that PC.
2. Create the agent session, for example `TEST agent session start`.
3. Record the session ID locally.
4. Install that agent's bridge script.
5. Configure local `.env` with Notion token.
6. Run bridge baseline.
7. Run bridge dry-run.
8. Register a local schedule, usually every 1 minute.
9. Post a `READY` message to Notion.

## Notes

- Do not route all remote agents through one central PC unless necessary.
- Local bridges are better for screenshots, file downloads, browser checks, and local repo state.
- Notion is the coordination layer; GitHub/project workspace is the artifact layer.

