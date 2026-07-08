# Runbook — Attach A New Project

Use this when Hermes should operate a project other than SafeRT.

## 1. Create Project Folder

```text
D:\AI_Hermes\projects\<project-name>
```

Copy from:

```text
D:\AI_Hermes\projects\_template
```

## 2. Define Project Workspace

Record:

- local repo/workspace path
- Git branch policy
- build/test commands
- source ownership rules

## 3. Define Notion Channels

Record:

- main agent channel page ID
- optional CH/v2 pages
- archive pages
- Notion integration access

Do not store tokens in this repo.

## 4. Choose Active Agents

For each active agent:

- role
- local computer
- runtime: Codex, Claude Code, other
- session id or local discovery method
- bridge script
- wake schedule

## 5. Create Kickoff Prompt

Place under:

```text
prompts/kickoff/<project>-<agent>.md
```

## 6. Create Continuity Pack

Place under:

```text
prompts/continuity/<project>-<agent>-continuity.md
```

## 7. Install Bridge

Prefer local bridge on the same computer as the agent session.

Remote operation is possible, but local bridge per PC is more robust for:

- file access
- browser screenshots
- local source inspection
- local tool permissions

## 8. Baseline

Before enabling a bridge:

```text
node hermes-<agent>-bridge.mjs --baseline
node hermes-<agent>-bridge.mjs --once --dry
```

This avoids flooding the agent with old messages.

