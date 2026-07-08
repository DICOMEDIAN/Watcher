# Skill: project-skillset-factory

## Purpose

Convert a project repository and its Notion documentation into a stable skill
catalog that all Hermes agents can understand by name.

This is the reusable factory. Do not hand-build a new skill universe from
scratch for every project.

## Korean Name

프로젝트 스킬셋 팩토리

## When To Use

Use this whenever a new project is attached to Hermes or when an existing
project's documentation has grown enough that agents need shared vocabulary.

Examples:

```text
SafeRT 스킬셋 만들어줘.
이 프로젝트 문서에서 agent들이 알아들을 skill list 뽑아줘.
새 Notion 프로젝트를 Hermes에 붙였으니 skill catalog 만들어줘.
```

## Inputs

- project repository path
- Notion root page or project page id
- existing docs directory
- agent role registry
- README / AGENTS.md / CLAUDE.md / PRD / ADR / SDS / UI guideline files
- mockup and verification artifacts
- issue board or task database if available

## Extraction Passes

### 1. Operating Contract Pass

Find files that tell agents how to behave:

- `AGENTS.md`
- `CLAUDE.md`
- `README.md`
- `CONTRIBUTING.md`
- Notion agent operation pages
- collaboration workflow docs

Output skill type: `*-agent-rules`, `*-workflow`, `*-handoff`, `*-issue-sync`.

### 2. Product Contract Pass

Find files that define what the product is:

- `PRD.md`
- PDR/PDD/product specs
- roadmap docs
- Notion planning pages
- user feedback pages

Output skill type: `*-prd`, `*-roadmap`, `*-user-evidence`.

### 3. Architecture Decision Pass

Find architectural records and system design:

- `ADR-*.md`
- `ARCHITECTURE.md`
- SDS/design specs
- database schema
- API contracts

Output skill type: `*-architecture`, `*-adr-*`, `*-api-contract`,
`*-data-contract`.

### 4. Domain Harness Pass

Find domain knowledge that agents must apply when judging correctness:

- standards
- domain glossaries
- regulation notes
- expert review notes
- external reference packs

Output skill type: `*-domain`, `*-regulatory`, `*-expert-review`.

### 5. UI/UX Harness Pass

Find reusable UI rules and mockup evidence:

- `UI_GUIDE.md`
- `UI_DESIGN_GUIDELINES.md`
- design tokens
- mockup folders
- screenshots
- UX handoffs

Output skill type: `*-ui-guideline`, `*-mockup-harness`,
`*-visual-gate`.

### 6. Verification Harness Pass

Find ways agents should prove that work is correct:

- test guides
- verification logs
- Playwright/MCP docs
- build/test/lint commands
- acceptance criteria
- preview/deploy rules

Output skill type: `*-validation`, `*-test-gate`, `*-build-gate`.

### 7. Notion Knowledge Pass

Read project Notion pages and collect:

- child page titles
- headings
- issue board fields
- message channels
- archive pages
- planning/ideation pages
- docs that exist only in Notion

Output skill type: `*-notion-workflow`, `*-planning-hub`,
`*-feedback-ledger`.

## Output Files

For each project:

```text
D:\AI_Hermes\projects\<project>\skills\SKILL-LIST.md
D:\AI_Hermes\projects\<project>\skills\SKILL-ALIASES.md
D:\AI_Hermes\projects\<project>\skills\SKILL-SOURCES.md
```

Optional runtime mirror:

```text
%HERMES_HOME%\skills\<project>-domain\<project>-skill-list\SKILL.md
```

## Skill Naming Rules

- Use lowercase kebab-case.
- Prefix project-specific skills with the project name.
- Prefer meaning over document names.
- Keep names short enough to say in chat.
- Add Korean aliases for human use.

Good:

```text
safert-dgmp-ui-guideline
safert-process-map-sot
safert-dev-test-handoff
```

Bad:

```text
docs-adr-006-risk-process-map-prozesskarte-md-reader
random-ui-stuff
```

## Skill Record Format

Each skill record should include:

```markdown
## skill-name

- Korean alias:
- Use when:
- Primary agents:
- Source docs:
- What agents should do:
- Output expected:
```

## Runtime Rule

Install a lightweight aggregate skill into Hermes runtime first. Install
individual detailed skills only when they become frequently invoked.

This avoids cluttering Hermes with dozens of rarely used project micro-skills
while still letting agents recognize skill names.

