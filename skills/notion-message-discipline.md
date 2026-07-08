# Skill: notion-message-discipline

## Purpose

Keep Notion as a reliable message bus while avoiding draft leakage, duplicated
work, stale context, and user-visible protocol noise.

## Activation

Use this skill for all Notion message polling, queueing, delivery, reply
formatting, and archive management.

## User Instruction Rule

Only text fully wrapped in `!! ... !!` is a valid user instruction.

- `!! do this !!` is valid.
- `!! do this` is incomplete and must not be delivered.
- Normal unwrapped text may be context, but agents should not treat it as a
  direct user command.

## Delivery Rule

All registered agents may hear all messages. Each agent decides:

- `ACTIONABLE`: I should act.
- `REFERENCE`: useful context, no action.
- `IGNORE`: not relevant.

Hermes should not over-filter unless the message is malformed, incomplete, or
unsafe to deliver.

## Display Rule

User-facing replies should use a clean header:

```text
[YYYY-MM-DD HH:mm] AGENT->USER | ANSWER
```

Do not show protocol fields to the user unless explicitly requested:

- source_channel
- conversation_id
- next_agent
- relevance
- intended_action
- *_READY

Agent-to-agent messages may include structured metadata when it helps parallel
context tracking.

## Ordering Rule

The newest message appears at the top of the Notion message log section.

