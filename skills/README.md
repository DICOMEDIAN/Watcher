# Hermes Operations Skillset

This folder defines reusable skills for operating the Hermes multi-agent team.

These are not project-specific source-code skills. They are operating skills:

- how Hermes reads Notion
- how messages become agent work
- how daily summaries are created
- how important facts are promoted to long-term memory
- how files/images move safely
- how encoding failures are prevented
- how new local or remote agents are attached

## Skill Tiers

```text
Tier 1: Always-on operating rules
  encoding-guardian
  notion-message-discipline

Tier 2: Scheduled Hermes jobs
  daily-summary
  memory-promotion
  archive-housekeeping

Tier 3: Agent/team expansion
  agent-onboarding
  remote-agent-attach
  notion-media-transfer

Tier 4: Multi-agent work cycles
  plan-development-cycle
  ideation-cycle
  development-validation-cycle
```

## Recommended Rollout Order

1. `encoding-guardian`
2. `notion-message-discipline`
3. `daily-summary`
4. `memory-promotion`
5. `notion-media-transfer`
6. `agent-onboarding`
7. `remote-agent-attach`
8. `ideation-cycle`
9. `plan-development-cycle`
10. `development-validation-cycle`
11. `project-skillset-factory`

## Storage Policy

Keep canonical skill descriptions here in Git. Install or mirror only the
active runtime skills into Hermes local skill storage.

This keeps the operating memory portable across PCs while allowing each machine
to run only the skills it needs.

## Cycle Skills

Cycle skills are reusable multi-agent workflows. A user should be able to say:

```text
Run ideation cycle 4 times.
Run development-validation cycle 3 times for this issue.
```

Hermes should then create structured rounds, wake the relevant agents, collect
their outputs, and synthesize the result through Smartie or the assigned
orchestrator.

## Project Skill Factory

`project-skillset-factory` is the reusable way to turn project documentation
into agent-callable skill names. Use it before creating one-off project skills.

It creates:

- a skill list
- aliases
- source map
- tag taxonomy
- harness templates
