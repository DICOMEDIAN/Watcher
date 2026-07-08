# Skill: development-validation-cycle

## Purpose

Drive an implementation issue through repeated development, review, test, and
fix loops until no known errors remain.

## Korean Name

개발-검수 사이클

## Agents

- DEV / 개발이: implementation, source edits, commits
- SMARTIE / 똑똑이: orchestration, prioritization, synthesis, feedback routing
- TEST / 투덜이: MCP-assisted functional and scenario testing on another PC
- SENSI / 센시: static code review and independent MCP verification when needed
- STEIN / 스타인: safety/regulatory/domain review when relevant
- MAX / 맥스: product/market impact review when relevant
- KKUMI / 꾸미: UX/visual/product feel review when relevant

## Cycle Shape

```text
Issue Intake:
  SMARTIE clarifies the issue, target branch, acceptance criteria, and test
  surface.

Development:
  DEV pulls latest changes, implements the fix or feature, runs local checks,
  and commits.

Review:
  SENSI performs static review. Other agents review when their domain applies.

Functional Test:
  TEST pulls the latest commit on another PC, connects by IP when needed, uses
  MCP/browser/runtime tools for unit-level and scenario validation, and checks
  console/log evidence.

Synthesis:
  SMARTIE collects findings and sends concrete fix feedback to DEV.

Repeat:
  Continue until requested cycle count is reached or no known blocking errors
  remain.
```

## Inputs

- issue description
- repository path and branch
- acceptance criteria
- target runtime or IP endpoint
- required test scope
- current Notion discussion

## Required Outputs

```markdown
## Cycle Result
## Commit
## DEV Changes
## Static Review
## Functional Test
## Scenario Test
## Console Or Log Evidence
## Remaining Errors
## Fix Feedback To DEV
## Final Acceptance State
```

## Git Rule

DEV is the default committer for implementation changes. Review and test agents
should not rewrite DEV's commit history. They may report patches or exact file
findings.

## Remote Test Rule

TEST may run on another PC. It should pull the latest commit, verify the exact
commit hash, and report environment, endpoint, evidence, and reproduction steps.

## Iteration Rule

When the user requests N cycles, run at most N full development-validation
rounds unless a hard blocker requires user input.

## Completion Rule

The cycle is complete when SMARTIE reports:

- latest commit hash
- errors found and fixed
- remaining known risks
- final acceptance status
- next owner, if work remains

