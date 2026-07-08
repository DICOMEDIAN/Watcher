# Multi-Project Notion Operation

Hermes can operate multiple projects and multiple Notion workspaces/pages.

Each project instance needs:

- Notion message log page IDs
- archive page IDs
- active agent list
- project workspace path
- bridge scripts or remote bridge runners
- message/archive policy

## Recommended Project Layout

```text
projects/<project-name>/
  project.md
  notion-channel-map.example.json
  active-agents.md
  bridge-bindings.md
  archive-policy.md
```

## Channel Roles

Typical channels:

- `agent`: main team and USER channel
- `CH`: general communication hub
- `v2` or project-specific channel

Do not hardcode SafeRT channel IDs in reusable templates.

## Archive Policy

Current default:

- If message log exceeds 100 blocks, keep newest 40.
- Archive older messages into a per-channel archive page.
- Group archive blocks by date toggle.
- Preserve image/file blocks where possible.

## Token Policy

Notion tokens are local secrets. Store in `.env` or machine-local secret storage, never in GitHub.

