# SafeRT Project Instance

SafeRT is the first project instance using this Hermes operation memory.

## Workspace

```text
C:\Users\user\SafeRTAgent\SafeRT
```

Branch:

```text
Agentic-SafeRT
```

## Current Local Agents

| Agent | Runtime | Bridge |
|---|---|---|
| SMARTIE | Claude Code | `safert_smartie_bridge.py` |
| DEV | Claude Code | `safert_dev_bridge.py` |
| STEIN | Codex | `safert_stein_bridge.py` |

## Current Remote/Other-PC Agents

- TEST / 투덜이
- SENSI / 센시
- MAX / 맥스
- KKUMI / 꾸미

These should be attached on their own computers with local bridge runners.

## Notion Channels

Known SafeRT channels at time of setup:

| Channel | Page ID |
|---|---|
| agent | `38c1a1ad-bebd-816c-8de1-d26514161b55` |
| CH | `3721a1ad-bebd-8112-a72c-e0e019d8cd5a` |
| v2 | `3741a1ad-bebd-813e-a0fc-d370479a86e5` |

Archive pages:

| Channel | Archive Page ID |
|---|---|
| agent | `38d1a1ad-bebd-8151-af52-c7327b6d6eca` |
| CH | `3721a1ad-bebd-81ab-9b41-c3e3be0d11b6` |
| v2 | `3791a1ad-bebd-8135-ad43-ed07ebf60baa` |

## Current Bridge Scripts

Repo-local:

- `tools/notion/hermes-smartie-bridge.mjs`
- `tools/notion/hermes-dev-bridge.mjs`
- `tools/notion/hermes-stein-bridge.mjs`
- `tools/notion/upload-outbox.mjs`
- `tools/notion/archive-if-needed.mjs`

Hermes-local wrappers:

- `C:\Users\user\AppData\Local\hermes\scripts\safert_smartie_bridge.py`
- `C:\Users\user\AppData\Local\hermes\scripts\safert_dev_bridge.py`
- `C:\Users\user\AppData\Local\hermes\scripts\safert_stein_bridge.py`

## Message Formatting

USER-facing:

```text
[YYYY-MM-DD HH:mm] AGENT→USER | ANSWER
```

Agent-to-agent:

```text
[YYYY-MM-DD HH:mm] FROM→TO | REVIEW/REPORT/HANDOFF
```

## SafeRT-Specific Role Boundary

- DEV writes code.
- TEST closes Done.
- STEIN does not edit code unless USER explicitly overrides.
- SMARTIE coordinates and plans.

