# AI Hermes Operations

This folder is the independent operating memory for a Hermes-based multi-agent team.

It is intentionally separate from any single product repository such as SafeRT. Use this folder to preserve:

- agent identities and role boundaries
- Hermes/Notion messaging policy
- bridge architecture and setup templates
- continuity packs and kickoff prompts
- project-specific Notion channel maps
- operational decisions and runbooks

Do not store secrets here.

## Core Idea

Hermes is the team operator. Notion is the shared message log. GitHub/project workspaces are project-specific.

```text
AI_Hermes
  core memory and bridge policy
  reusable agent templates
  reusable Notion/channel rules
  project instances

Project workspace
  source code
  tests
  project docs
  local agent session

Notion
  live messages
  attachments
  archive pages
```

## Current Local Agents

This PC currently has three local agents attached through Hermes:

- SMARTIE / 똑똑이
- DEV / 개발이
- STEIN / 스타인

Other agents can run on other computers with their own Hermes or bridge runner:

- TEST / 투덜이
- SENSI / 센시
- MAX / 맥스
- KKUMI / 꾸미

## Directory Map

```text
agents/              reusable agent identity docs
bridges/             bridge architecture and implementation notes
memory/              durable decisions and policies
notion/              Notion messaging/archive policies
projects/            project-specific instances
prompts/             kickoff and continuity prompts
runbooks/            setup and recovery procedures
skills/              reusable Hermes skill notes
status/              local runtime status snapshots
templates/           project/agent templates
```

## Must-Read Runbooks

- [Install And Setup From Zero](runbooks/install-and-setup.md)
- [Install Codex And Claude](runbooks/install-codex-and-claude.md)
- [Attach Remote Agent PC](runbooks/attach-remote-agent-pc.md)
- [Remote Agent Session Kickoff](runbooks/remote-agent-session-kickoff.md)
- [Remote PC Quick Checklist](runbooks/remote-pc-quick-checklist.md)
- [Notion Messaging Rules](notion/messaging-rules.md)
- [Encoding Survival Guide](memory/encoding-survival-guide.md)
- [Message Format And Media Handling](notion/message-format-and-media.md)

## Secret Policy

Never commit or sync:

- Notion API tokens
- OpenAI/Claude/Gemini/Ollama keys
- `.env`
- Hermes `state.db`, `kanban.db`, lock files, or runtime DBs
- raw Codex/Claude auth files
- private local session transcripts unless intentionally sanitized
