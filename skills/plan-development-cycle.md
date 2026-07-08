# Skill: plan-development-cycle

## Purpose

Turn a planning draft into a stronger product/development proposal through a
multi-agent dialectic cycle.

## Korean Name

기획안 발전 사이클

## Agents

- SMARTIE / 똑똑이: primary planner and synthesis owner
- SENSI / 센시: co-planner, mockup and critique owner
- MAX / 맥스: market, strategy, and opportunity critique
- STEIN / 스타인: safety, regulation, evidence, and risk critique
- DEV / 개발이: implementation feasibility and technical cost critique
- KKUMI / 꾸미: user experience, visual, product feeling critique

## Cycle Shape

```text
Thesis:
  SMARTIE and SENSI deepen the initial plan and create a mockup or concrete
  planning artifact.

Antithesis:
  MAX, STEIN, SENSI, DEV, KKUMI, and SMARTIE each submit 10 problems from their
  own perspective, using different review methods where useful.

Dialectic:
  Agents discuss conflicts, tradeoffs, and overlapping concerns.

Synthesis:
  SMARTIE produces the next combined plan, including decisions, unresolved
  questions, and handoffs.
```

## Inputs

- user prompt or seed idea
- existing plan draft
- screenshots, files, or mockups if available
- project constraints
- target users
- current open issues

## Required Outputs

```markdown
## Cycle Result
## Updated Plan
## Mockup Notes
## Top 10 Consolidated Problems
## Agent-Specific Findings
## Synthesis
## Decisions
## Open Questions
## Next Handoffs
```

## Iteration Rule

When the user requests N cycles, each cycle must use the previous synthesis as
the next thesis.

## Completion Rule

The cycle is complete when SMARTIE writes a synthesis that identifies:

- what changed in the plan
- which objections were accepted or rejected
- what DEV should build next, if anything
- what evidence is still missing

