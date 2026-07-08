# Notion Message Format And Media Handling

## Message Headers

### USER-Facing Answer

```text
[YYYY-MM-DD HH:mm] AGENT→USER | ANSWER
본문
```

### Agent-To-Agent Review

```text
[YYYY-MM-DD HH:mm] SENSI→DEV | REVIEW
Findings first.

1) P2 / title...
```

### Ready

```text
[YYYY-MM-DD HH:mm] AGENT→USER | READY
AGENT_READY
short human-readable readiness note
```

## Header Types

Recommended:

- `ANSWER`
- `READY`
- `REPORT`
- `REVIEW`
- `HANDOFF`
- `REQUEST`
- `VERDICT`
- `NOTE`

## USER-Facing Body

Strip bridge metadata from visible body:

- `*_READY`
- `received_from`
- `source_channel`
- `conversation_id`
- `relevance`
- `next_agent`
- `intended_action`

Internal fields can remain in bridge state or agent prompts.

## File/Image Download

When Notion message log contains:

- `image`
- `file`
- `pdf`

Bridge should:

1. download the file
2. save under `tools/notion/inbox-files/hermes-<agent>/`
3. include local path in agent prompt
4. include content type and size
5. instruct agent to inspect before judging

Prompt fields:

```text
- local_media_path: <path>
- media_content_type: <type>
- media_bytes: <bytes>
```

## File/Image Upload

Agents do not call Notion API directly.

Agents write upload manifests:

```text
tools/notion/outbox-files/<agent>/*.json
```

Manifest shape:

```json
{
  "channel": "agent",
  "from": "STEIN",
  "to": "USER",
  "type": "REPORT",
  "text": "Short explanation",
  "files": [
    "C:\\absolute\\path\\artifact.png"
  ]
}
```

Hermes runs:

```text
upload-outbox.mjs --agent <agent>
```

and appends file/image blocks to Notion.

## Upload Rules

- Use absolute file paths.
- Preserve extensions.
- Images should appear directly in Notion where possible.
- Other files should appear as file blocks.
- Captions should identify agent and purpose.
- If upload fails, move manifest to failed state or leave a clear error.

## Download Rules

- Download files before asking agent to judge image/file content.
- Do not ask agent to infer from caption alone when image/file is available.
- For screenshots, the local path is evidence.

## Media And Encoding

Captions may contain Korean/German. Treat captions as UTF-8.

Avoid raw emoji in captions generated from shell scripts; use Node codepoint construction if needed.

