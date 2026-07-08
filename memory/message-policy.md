# Hermes Message Policy

## Message Classes

### USER To Agent

Valid only when wrapped:

```text
!! user instruction !!
```

Incomplete draft:

```text
!! user is still typing
```

Do not deliver incomplete drafts as instructions.

### Agent To USER

Keep it readable.

```text
[2026-07-08 17:12] STEIN→USER | ANSWER
Natural answer only.
```

Do not show:

- routing metadata
- readiness fields
- conversation IDs
- source channel
- relevance labels
- next-agent fields

### Agent To Agent

Structured messages are allowed.

```text
[2026-07-08 01:11] SENSI→DEV | REVIEW
Findings first.

1) P2 / finding title...
```

Allowed when helpful:

- severity
- target agent
- review type
- conversation/thread short ID
- file paths
- evidence references

### Debug/Audit

Full Notion block IDs and bridge state belong in bridge logs/state files, not normal USER-visible text.

## Header Types

Suggested types:

- `ANSWER`
- `REPORT`
- `REVIEW`
- `HANDOFF`
- `VERDICT`
- `REQUEST`
- `READY`
- `NOTE`

## Highlight Rule

If an agent-to-agent thread produces a message intended for USER, the header must clearly target USER:

```text
[YYYY-MM-DD HH:mm] AGENT→USER | ANSWER
```

This prevents USER-directed messages from being buried in agent chatter.

