# Encoding Survival Guide

This is one of the most important Hermes operating documents.

Korean, German, arrows, and emoji can be corrupted when messages cross:

```text
Notion -> Node -> Python -> PowerShell -> Codex/Claude CLI -> Notion
```

The system must be engineered so this never silently breaks communication.

## Golden Rules

1. Use UTF-8 explicitly.
2. Prefer stdin over command-line prompt arguments.
3. Prefer Node/Python UTF-8 APIs over PowerShell text interpolation.
4. Do not trust default Windows console decoding.
5. If text displays as `???` or mojibake, re-read with explicit UTF-8 before judging.
6. Avoid raw emoji in scripts; use codepoints.

## Windows Environment

Gateway and bridge wrappers should set:

```text
PYTHONUTF8=1
PYTHONIOENCODING=utf-8
LANG=C.UTF-8
LC_ALL=C.UTF-8
NODE_DISABLE_COLORS=1
NO_COLOR=1
NODE_NO_WARNINGS=1
```

For `.cmd` gateway:

```bat
chcp 65001 >nul
```

## PowerShell File Reads

Always:

```powershell
Get-Content -LiteralPath <file> -Encoding UTF8 -Raw
```

Never rely on default `Get-Content` for Korean/German files.

## Prompt Delivery

Bad:

```text
claude --print "<long Korean prompt>"
codex exec resume <session> "<long Korean prompt>"
```

Good:

```text
prompt -> stdin
```

Codex:

```text
codex exec resume --output-last-message <output-file> <session-id> -
```

Claude:

Use stdin or a UTF-8 prompt file read explicitly as UTF-8.

## Emoji

Do not write raw emoji in shell scripts if avoidable.

Use codepoints:

```js
const steinIcon = String.fromCodePoint(0x1F9D4, 0x1F3FB, 0x200D, 0x2642, 0xFE0F)
```

## JSON

When parsing JSON manifests, strip UTF-8 BOM:

```js
JSON.parse(text.replace(/^\uFEFF/, ''))
```

PowerShell may create BOM-marked files.

## Test Cases

Always verify with:

```text
한글 정상
Deutsch äöüß
STEIN→USER
emoji via codepoint
```

Expected behavior:

- Notion stores text correctly.
- Bridge prompt file stores text correctly.
- Agent receives text correctly.
- Agent response returns to Notion correctly.

## Failure Interpretation

If raw emoji or Korean is corrupted during manual testing, first suspect the test injection method.

Known safe method:

- Node script
- Unicode escapes or `String.fromCodePoint`
- stdin to Codex/Claude

Known risky method:

- PowerShell here-string embedded in a shell command
- default `Get-Content`
- command-line prompt argument with long Korean text

