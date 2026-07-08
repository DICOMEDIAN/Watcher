# Remote PC Quick Checklist

Use this as the short checklist after reading
`runbooks/attach-remote-agent-pc.md`.

## Checklist

- [ ] Git installed
- [ ] Node.js installed
- [ ] Python installed
- [ ] Codex or Claude installed and logged in
- [ ] `Watcher` cloned
- [ ] Project repo cloned, if needed
- [ ] Local `.env` configured
- [ ] UTF-8 environment set
- [ ] Agent session created
- [ ] Kickoff prompt pasted
- [ ] Required Watcher docs read
- [ ] Required project docs read
- [ ] Bridge baseline run
- [ ] Bridge dry run passed
- [ ] Korean UTF-8 Notion test passed
- [ ] File/image Notion test passed or explicitly deferred
- [ ] Schedule registered
- [ ] READY posted to Notion

## Ready Message Template

```text
[YYYY-MM-DD HH:mm] <AGENT>->USER | READY
<AGENT>_READY
host: <pc-name>
project: <project>
skills_loaded: <skill ids>
utf8_test: pass
file_test: pass/fail/not-run
source_access: yes/no
```

