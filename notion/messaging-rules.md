# Notion Messaging Rules

## Core Model

Hermes does not wait for agents to poll Notion themselves.

Hermes:

1. reads Notion message logs
2. queues relevant new messages
3. wakes registered local agents through bridges
4. delivers a compact context package
5. receives the agent's reply
6. writes back to Notion

Each agent hears the shared conversation, but each agent decides whether a message is actionable for its role.

## Hear Everything, Respond Selectively

Default policy:

- every registered agent may receive every new message
- agents classify messages as `ACTIONABLE`, `REFERENCE`, or `IGNORE`
- agents respond only when named, targeted, or role-relevant

This prevents hidden context splits while avoiding noisy responses.

## USER Message Rule

Only text fully wrapped as:

```text
!! ... !!
```

is a USER instruction.

Examples:

```text
!! 개발아 이 버그 수정해줘 !!
```

Valid.

```text
!! 개발아 이 버그
```

Invalid incomplete draft. Do not deliver as USER instruction.

## Agent-To-Agent

Agent-to-agent messages may be structured:

```text
[2026-07-08 01:11] SENSI→DEV | REVIEW
Findings first.

1) P2 / finding...
```

Structure is useful for:

- review findings
- handoffs
- build/test reports
- evidence references
- parallel coordination

## Agent-To-USER

USER-facing messages should be clean:

```text
[2026-07-08 17:12] STEIN→USER | ANSWER
Natural answer body.
```

Do not show routine bridge metadata:

- `source_channel`
- `conversation_id`
- `relevance`
- `next_agent`
- `received_from`
- `*_READY`

## Conversation ID

Hermes may include `conversation_id` inside internal prompts to help agents align parallel context.

Do not show it to USER unless it materially helps:

- conflict resolution
- audit
- debugging
- multiple simultaneous requests with ambiguous replies

## Read/Unread Responsibility

Hermes tracks delivery state, but agents are responsible for judgment.

The bridge may mark a message delivered after the local session receives it. The agent still decides:

- whether it saw enough evidence
- whether to act
- whether to ask for more evidence
- whether to ignore as not role-relevant

## Newest On Top

Message log UI should keep newest messages near the top under the message-log heading when possible.

This makes active communication easier to scan.

## Archiving

To reduce Notion API load:

- when a channel exceeds 100 message-log blocks
- keep newest 40
- archive older blocks by date toggle
- preserve files/images where possible

