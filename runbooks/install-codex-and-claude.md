# Runbook — Install Codex And Claude Agent Runtimes

Hermes can wake different agent runtimes. Current proven runtimes are Codex and Claude Code.

## Codex

Use Codex when:

- the agent should run as a Codex session
- `codex exec resume <session-id> -` is available
- final response can be captured with `--output-last-message`

### Verify Codex

```powershell
codex --version
codex exec --help
codex exec resume --help
```

Expected bridge invocation:

```powershell
codex exec resume --output-last-message <output-file> <session-id> -
```

Prompt body is sent through stdin.

Do not pass Korean/German prompt text as a command-line argument.

### Start A Codex Agent Session

Open project workspace in Codex or VSCode/Codex extension, then start:

```text
STEIN agent session start
```

After the session exists, find the session ID from Codex session index/logs and configure the bridge.

## Claude Code

Use Claude Code when:

- the agent already runs as a Claude Code session
- `claude --resume <session-id> --print` is available
- the bridge can capture stdout

### Verify Claude

```powershell
claude --version
claude --help
```

Expected bridge invocation:

```powershell
claude --resume <session-id> --permission-mode acceptEdits --print
```

Prompt body should be passed through stdin or a UTF-8 prompt file read explicitly as UTF-8.

Do not pass long Korean/German prompts as command-line arguments.

## Session Discovery

Codex sessions are usually under:

```text
C:\Users\<user>\.codex\sessions
C:\Users\<user>\.codex\session_index.jsonl
```

Claude sessions are usually under:

```text
C:\Users\<user>\.claude\projects\<project-key>\*.jsonl
```

Search by initial title:

```text
STEIN agent session start
Dev agent session start
```

## Runtime Rule

The bridge must run on the same PC as the local agent session unless there is a strong reason not to.

Local bridge is better for:

- source inspection
- screenshots
- file downloads/uploads
- browser checks
- local tool permissions

