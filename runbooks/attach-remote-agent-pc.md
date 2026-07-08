# Runbook — Attach An Agent On Another PC

Recommended model: each PC runs its own Hermes or lightweight bridge runner for
its local agent session.

```text
Remote PC agent session
  -> local bridge / local Hermes
  -> Notion channels
  -> other agents
```

Do not depend on one central Windows PC unless there is a clear reason. Notion is
the shared coordination layer. GitHub is the project artifact layer. `Watcher`
is the operating memory and skill catalog.

## 0. What The Remote Session Must Achieve

By the end, the remote agent should be able to:

- read the project skill catalog from `Watcher`
- read the project source if its role requires it
- read/write the correct Notion channel
- receive only complete USER instructions wrapped in `!! ... !!`
- preserve UTF-8 Korean/German text
- download referenced files/images when needed
- post a `READY` message
- run its assigned role without using the legacy watcher bus

## 1. Required Local Software

Install on the remote PC:

- Git
- Node.js LTS or newer
- Python 3.11+
- Codex or Claude Code, depending on the agent
- Hermes Agent, or a lightweight bridge runner
- project-specific tools, such as browser/MCP/test tooling

For SafeRT development/testing PCs, also install the project build/runtime
dependencies described by the project repo.

## 2. Clone The Hermes Operating Memory

Recommended path:

```text
D:\AI_Hermes
```

Windows:

```powershell
git clone https://github.com/DICOMEDIAN/Watcher.git D:\AI_Hermes
cd D:\AI_Hermes
git status
```

macOS/Linux:

```bash
git clone https://github.com/DICOMEDIAN/Watcher.git ~/AI_Hermes
cd ~/AI_Hermes
git status
```

Read first:

```text
README.md
memory/message-policy.md
memory/encoding-survival-guide.md
skills/README.md
projects/<project>/project.md
projects/<project>/skills/SKILL-LIST.md
projects/<project>/skills/SKILL-ALIASES.md
projects/<project>/skills/SKILL-METADATA.yaml
```

## 3. Clone Or Open The Project Workspace

If the agent needs source access, clone the project repository locally.

SafeRT example:

```powershell
git clone https://github.com/DICOMEDIAN/SafeRT.git C:\Users\<user>\SafeRTAgent\SafeRT
cd C:\Users\<user>\SafeRTAgent\SafeRT
git checkout Agentic-SafeRT
git pull
```

The exact branch may vary by project. Check:

```text
D:\AI_Hermes\projects\<project>\project.md
```

## 4. Configure Local Secrets

Create machine-local Hermes/project `.env` files. Never commit them.

Required for Notion:

```text
NOTION_TOKEN=...
NOTION_API_KEY=...
NOTION_API_TOKEN=...
NOTION_KEYRING=0
```

Use only the token values provided by the user or local secret manager.

## 5. Enforce UTF-8 Before Any Bridge Test

Windows bridge shells should set:

```bat
chcp 65001 >nul
set "PYTHONUTF8=1"
set "PYTHONIOENCODING=utf-8"
set "LANG=C.UTF-8"
set "LC_ALL=C.UTF-8"
set "NODE_DISABLE_COLORS=1"
set "NO_COLOR=1"
```

macOS/Linux shells should set:

```bash
export PYTHONUTF8=1
export PYTHONIOENCODING=utf-8
export LANG=C.UTF-8
export LC_ALL=C.UTF-8
export NODE_DISABLE_COLORS=1
export NO_COLOR=1
```

Encoding rule:

```text
If Korean becomes ??? or mojibake, stop. Do not forward the message.
Fix encoding before continuing.
```

## 6. Mirror The Runtime Skills

`Watcher` stores canonical skill definitions. Each PC may mirror only the active
runtime skills into its local Hermes skill directory.

Minimum remote PC skills:

```text
encoding-guardian
notion-message-discipline
project-skillset-factory
safert-skill-list, for SafeRT
```

If using Hermes runtime, create a local aggregate skill from the project catalog.

SafeRT runtime skill identity:

```text
safert-domain / safert-skill-list
```

Source of truth:

```text
projects/safert/skills/SKILL-LIST.md
projects/safert/skills/SKILL-ALIASES.md
projects/safert/skills/SKILL-METADATA.yaml
projects/safert/skills/HARNESS-RECIPES.md
```

The remote session should not invent new skill names before checking
`SKILL-ALIASES.md`.

## 7. Start The Agent Session

Create a clear session title:

```text
SENSI agent session start
TEST agent session start
MAX agent session start
KKUMI agent session start
```

Then paste the remote-agent kickoff prompt from:

```text
runbooks/remote-agent-session-kickoff.md
```

Record the local session id in a private machine-local note. Do not commit
session ids to public repos.

## 8. Bind The Agent Role

Update the local bridge config with:

- canonical agent id
- Korean call name
- English call name
- runtime type
- project path
- Notion channels
- bridge state file
- inbox/outbox file paths
- wake interval

Use:

```text
agents/agent-registry.md
projects/<project>/project.md
projects/<project>/skills/SKILL-LIST.md
```

## 9. Run Bridge Baseline

Baseline means: mark current old messages as already seen, without acting.

The exact command depends on the bridge implementation. The expected behavior:

```text
read Notion channels
record seen block ids
do not wake the agent
do not reply
do not archive
```

## 10. Run Dry Test

Dry test means: read new candidate messages and print what would be delivered,
without writing to the agent session or Notion.

Check:

- only complete `!! ... !!` USER messages are actionable
- incomplete `!!` drafts are ignored
- Korean text is intact
- attachments are detected
- all agents can hear messages, but role decides whether to act

## 11. Run Live UTF-8 Test

Post from Notion:

```text
!! <AGENT>, 한글 한 문장으로 수신 확인해줘. !!
```

Expected reply:

```text
[YYYY-MM-DD HH:mm] AGENT->USER | ANSWER
...
```

No `source_channel`, `conversation_id`, `relevance`, `next_agent`, or internal
status noise should be shown to the user.

## 12. Run File/Image Test

Post a small image or file in Notion and ask:

```text
!! <AGENT>, 방금 올린 파일/그림을 받았는지만 확인해줘. 내용 판단은 하지마. !!
```

The agent should report:

- local downloaded path
- file name
- file type if known
- whether it can access it

The agent should not embed raw binary in the prompt.

## 13. Register Schedule

Recommended default:

```text
bridge: every 1 minute
queue broker: every 5 minutes, if used on that PC
archive/daily summary: usually central PC only, unless explicitly distributed
```

Remote PCs usually need only their own bridge. Avoid duplicated archive jobs
unless a project has intentionally assigned ownership.

## 14. Post READY

When complete, post to the correct Notion channel:

```text
[YYYY-MM-DD HH:mm] <AGENT>->USER | READY
<AGENT>_READY
host: <pc-name>
project: <project>
skills_loaded: <list>
utf8_test: pass
file_test: pass/fail/not-run
source_access: yes/no
```

USER-facing bridges may hide protocol noise later, but during setup the READY
message may include setup details.

## 15. Ongoing Rule For The Remote Agent

Every work turn starts with:

1. Pull latest `Watcher`.
2. Pull latest project repo if source access is needed.
3. Read relevant skill aliases.
4. Read current Notion queue/messages.
5. Decide `ACTIONABLE`, `REFERENCE`, or `IGNORE`.
6. Act only if the role is responsible.
7. Report with evidence and next owner.

## 16. SafeRT-Specific Minimum Reading

For a SafeRT remote agent, read:

```text
projects/safert/project.md
projects/safert/skills/SKILL-LIST.md
projects/safert/skills/SKILL-ALIASES.md
projects/safert/skills/HARNESS-RECIPES.md
projects/safert/skills/KNOWLEDGE-INVENTORY.md
```

If source repo is available, also read:

```text
CLAUDE.md
AGENTS.md
docs/PRD.md
docs/COLLABORATION_WORKFLOW.md
```

Role-specific:

- TEST: `safert-dev-test-handoff`, `safert-excel-fidelity`, `safert-risk-prozesskarte`
- SENSI: `safert-dgmp-ui-guideline`, `safert-mockup-harness`, `safert-ui-branch-gate`
- STEIN: `safert-fmea-risk-domain`, `safert-german-report-compliance`, `safert-sae-sync-contract`
- MAX: `safert-prd`, `safert-beta-pilot-evidence`, `safert-ai-jury-consensus`
- KKUMI: `safert-dgmp-ui-guideline`, `safert-mockup-harness`

