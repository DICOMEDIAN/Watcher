# Skill: project-skill-metadata-taxonomy

## Purpose

Define metadata and tags for project skills so agents can find the right lens
and generate harnesses quickly.

## Metadata Fields

Each project skill should have:

```yaml
id:
project:
name:
korean_aliases:
english_aliases:
category:
tags:
primary_agents:
secondary_agents:
source_docs:
notion_sources:
runtime_inputs:
expected_outputs:
harness_types:
risk_level:
hot_memory_candidate:
last_reviewed:
```

## Category Tags

Use these high-level categories:

```text
agent-ops
product
architecture
domain
ui-ux
data-contract
import-export
regulatory
testing
deployment
notion-workflow
mockup
user-evidence
ai-rag
security
```

## Harness Type Tags

Use these when a skill can generate a reusable harness:

```text
review-harness
test-harness
ui-harness
regulatory-harness
data-fidelity-harness
mockup-harness
notion-workflow-harness
deployment-harness
evidence-harness
```

## Risk Level

```text
P0: safety, regulatory, data loss, security, irreversible corruption
P1: major user workflow, build failure, cross-agent coordination failure
P2: normal product correctness or UX quality
P3: polish, documentation, optional improvement
```

## Hot Memory Rule

Only promote a skill fact into Hermes hot memory if it changes behavior across
most future sessions.

Examples:

- Good hot memory: "SafeRT uses !!...!! as complete USER instruction signal."
- Good hot memory: "SafeRT DEV must not mark Notion issues Done; TEST owns Done."
- Not hot memory: every individual ADR detail.

