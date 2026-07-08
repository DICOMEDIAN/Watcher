# Bridge Architecture

Hermes bridges connect Notion messages to local agent sessions.

## Pattern

```text
Notion message log
  -> Hermes scheduled bridge
  -> local agent session
  -> bridge captures final output
  -> Notion writeback
```

## Current Local Bridge Types

### Claude Code Bridge

Used by SMARTIE and DEV.

Prompt delivery:

- Write UTF-8 prompt file.
- Send prompt to Claude via stdin or safe invocation.
- Avoid long command-line prompt arguments.

### Codex Bridge

Used by STEIN.

Prompt delivery:

```text
codex exec resume --output-last-message <output-file> <session-id> -
```

The prompt is sent through stdin. The final answer is read from `--output-last-message`.

## Writeback Policy

For USER-facing replies, strip agent metadata and use:

```text
[YYYY-MM-DD HH:mm] AGENT→USER | ANSWER
```

For agent-to-agent replies, structured review/report headers are allowed.

## Internal Context Fields

Bridges may include these in prompts to agents:

- `conversation_id`
- Notion block ID
- source channel
- block type
- local media path
- media content type
- media byte count
- whether text is a valid USER `!! ... !!` message

Most of these fields should not be shown to USER.

## Media Handling

For Notion image/file/pdf blocks:

- download to `tools/notion/inbox-files/hermes-<agent>/`
- include local path in agent prompt
- require agent to inspect media before judging

## Upload Handling

Agents should not call Notion APIs directly.

Agents create manifests under:

```text
tools/notion/outbox-files/<agent>/*.json
```

Hermes uploads files using `upload-outbox.mjs`.

