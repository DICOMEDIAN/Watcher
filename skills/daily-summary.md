# Skill: daily-summary

## Purpose

Create a daily operational summary from Notion message logs before the raw
message history becomes too large or is archived.

## Schedule

Recommended Hermes cron timing:

```text
00:10 local time, once per day
```

The job must either:

- run before archive housekeeping, or
- read both live message logs and archive pages.

## Inputs

- Notion live message logs
- Notion archive pages
- downloaded attachment metadata
- bridge delivery logs
- current agent registry

## Output

Write a markdown file:

```text
D:\AI_Hermes\daily\YYYY-MM-DD.md
```

## Required Sections

```markdown
# Daily Summary - YYYY-MM-DD

## Channels
## Main Events
## Agent Activity
## Decisions
## Files And Images
## Encoding Incidents
## Open Threads
## Memory Promotion Candidates
```

## Git Rule

After writing the summary, commit it to the Watcher repository unless the
working tree contains unrelated manual edits.

