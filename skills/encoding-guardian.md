# Skill: encoding-guardian

## Purpose

Prevent Korean, emoji, file names, Notion text, and JSON payloads from being
corrupted while Hermes, Notion, Claude, Codex, Node, Python, and PowerShell
exchange messages.

## Activation

Use this skill whenever a task touches:

- Notion message reads or writes
- Claude/Codex bridge prompts
- JSON manifests
- file/image upload or download metadata
- PowerShell commands containing non-ASCII text
- agent replies that may contain Korean or symbols

## Rules

- Use UTF-8 end to end.
- Set `PYTHONUTF8=1` and `PYTHONIOENCODING=utf-8` for Python bridge jobs.
- Prefer Node/Python UTF-8 file APIs over command-line string arguments.
- Avoid raw Korean/emoji in shell commands.
- Pass non-ASCII payloads through stdin, JSON files, or codepoints.
- Strip UTF-8 BOM before parsing JSON.
- Treat any `???`, mojibake, or replacement characters as a hard failure.
- Test Korean and emoji separately before trusting a new bridge path.

## Failure Response

When encoding corruption is detected:

1. Stop forwarding that message.
2. Preserve the raw input if possible.
3. Write a diagnostic entry to the bridge log.
4. Ask for retransmission only after the path is fixed.

## Promotion Rule

Any new encoding failure and its fix should be promoted to:

- `D:\AI_Hermes\memory\encoding-survival-guide.md`
- daily summary for that date
- Hermes hot memory only if it changes future behavior

