# Runbook — Install And Setup From Zero

This runbook is project-independent. Use it when preparing a new PC for Hermes multi-agent operation.

## 0. Goal

The PC should be able to:

- run Hermes
- connect to Notion
- run one or more local agent sessions
- wake those agents from Notion messages
- upload agent replies/files/images back to Notion
- preserve UTF-8 Korean/German text without corruption

## 1. Required Software

Install:

- Git
- Node.js LTS or newer
- Python 3.11+
- Codex CLI / Codex extension where needed
- Claude Code where needed
- Hermes Agent
- optional: Ollama, browser tooling, project-specific build tools

## 2. Workspace Layout

Recommended:

```text
D:\AI_Hermes
  Hermes operation memory

C:\Users\<user>\<ProjectRoot>
  project repositories

C:\Users\<user>\AppData\Local\hermes
  Hermes runtime/config/secrets
```

Do not put secrets into `D:\AI_Hermes`.

## 3. Hermes Install

Install Hermes Agent from the selected source and keep its runtime under:

```text
C:\Users\<user>\AppData\Local\hermes
```

Expected important files:

```text
config.yaml
.env
hermes-agent/
scripts/
cron/jobs.json
gateway-service/
```

## 4. Configure Environment

Machine-local `.env` should contain required tokens, for example:

```text
NOTION_API_KEY=...
NOTION_API_TOKEN=...
NOTION_KEYRING=0
```

Never commit `.env`.

## 5. Enable UTF-8 In Gateway

Windows gateway scripts must set UTF-8 explicitly:

```bat
chcp 65001 >nul
set "PYTHONUTF8=1"
set "PYTHONIOENCODING=utf-8"
set "LANG=C.UTF-8"
set "LC_ALL=C.UTF-8"
set "NODE_DISABLE_COLORS=1"
set "NO_COLOR=1"
```

## 6. Create Project Instance

Copy:

```text
D:\AI_Hermes\projects\_template
```

to:

```text
D:\AI_Hermes\projects\<project-name>
```

Fill:

- project workspace path
- Notion channel IDs
- archive page IDs
- active agents
- bridge bindings
- role boundaries

## 7. Create Agent Session

Open the project workspace in Codex or Claude Code and create the agent session:

```text
<AGENT> agent session start
```

Record the session ID in a local/private note. Do not publish it in a public repo.

## 8. Install Bridge

For each local agent:

1. create `hermes-<agent>-bridge.mjs`
2. run baseline
3. run dry-run
4. create Hermes wrapper script
5. register cron

Example:

```text
node hermes-stein-bridge.mjs --baseline
node hermes-stein-bridge.mjs --once --dry
```

Cron:

```text
every 1m
```

## 9. Post READY

When the bridge is ready, post a Notion READY message:

```text
[YYYY-MM-DD HH:mm] AGENT→USER | READY
AGENT_READY ...
```

## 10. Verify

Use a real USER message:

```text
!! AGENT, reply with one short Korean sentence if you received this. !!
```

Verify:

- message is delivered
- Korean is not corrupted
- answer is written to Notion
- metadata is hidden from USER-facing answer
- bridge state marks the message delivered

