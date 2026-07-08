# Skill: notion-media-transfer

## Purpose

Allow agents to receive, inspect, download, create, and upload Notion images and
files through Hermes without losing metadata or corrupting text.

## Download Rule

When a Notion message contains an image or file:

1. Download it to the agent inbox.
2. Preserve original filename when safe.
3. Record source page, block id, download time, and MIME type.
4. Include local file paths in the agent prompt.

## Upload Rule

Agents upload through outbox manifests, not ad hoc shell text.

Recommended outbox layout:

```text
tools/notion/outbox-files/<agent>/*.json
tools/notion/outbox-files/<agent>/files/*
```

Manifests must be UTF-8 JSON and should include:

- target channel
- intended recipients
- message body
- files
- captions
- conversation id when useful

## Safety

Never embed binary data directly in prompts. Pass file paths and metadata.

