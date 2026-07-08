# Durable Decisions

## 2026-07-08 — Hermes Ops Is Project-Independent

Hermes operating memory must not be tied to SafeRT only.

SafeRT is one project instance. Future projects may use different GitHub repositories, different Notion pages, and different agent teams while reusing the same Hermes operating policies.

## 2026-07-08 — Notion Is The Message Bus

The old watcher/message bus is historical only.

Current rule:

- Hermes reads Notion message logs.
- Hermes delivers messages to local agent sessions through bridges.
- Agents write back to Notion through Hermes-controlled writeback/outbox paths.
- Agents do not ask for Notion API tokens.

## 2026-07-08 — USER Message Boundary

Only text fully wrapped as `!! ... !!` is a USER instruction.

If text starts with `!!` but does not end with `!!`, it is an incomplete draft and must not be delivered as a USER instruction.

## 2026-07-08 — USER-Facing Messages Are Clean

USER-facing Notion replies should not expose routing metadata.

Hide from USER:

- `*_READY`
- `source_channel`
- `conversation_id`
- `relevance`
- `next_agent`
- `received_from`
- other bridge/debug fields

Use readable headers:

```text
[YYYY-MM-DD HH:mm] AGENT→USER | ANSWER
```

## 2026-07-08 — Agent-to-Agent Messages May Keep Structure

Agent-to-agent messages may keep structured headers and findings:

```text
[YYYY-MM-DD HH:mm] SENSI→DEV | REVIEW
Findings first.
```

Message IDs and conversation IDs are shown only when they materially help parallel coordination, conflict resolution, audit, or debugging.

## 2026-07-08 — Conversation IDs Are Internal

Hermes bridge prompts include `conversation_id` for agent-agent context alignment.

The ID is hidden from USER-facing answers unless explicitly needed.

## 2026-07-08 — UTF-8 Is Mandatory

Korean, German, and emoji must survive every bridge boundary.

Rules:

- Prefer Node/Python UTF-8 APIs.
- On Windows PowerShell, use `Get-Content -Encoding UTF8`.
- Do not pass long Korean prompts as command-line arguments.
- Prefer stdin or UTF-8 prompt files.
- Avoid raw emoji in shell scripts; use codepoints when needed.

The detailed operational guide is `memory/encoding-survival-guide.md`.

## 2026-07-08 — Role Boundaries

Default team boundaries:

- DEV writes code.
- TEST verifies and closes Done.
- SMARTIE plans, coordinates, and prioritizes.
- STEIN gives regulatory/safety judgment and evidence orders.
- SENSI reviews UX/design and can inspect screenshots.
- MAX gives buyer/hospital workflow perspective.
- KKUMI supervises visual system details.

Project-specific overrides must be recorded under `projects/<name>/`.
