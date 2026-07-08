# SafeRT Harness Recipes

These recipes turn SafeRT skills into reusable work harnesses.

## safert-excel-fidelity-test-harness

Based on:

- `safert-excel-fidelity`
- `safert-process-map-sot`
- `safert-sae-sync-contract`

Use when:

- Excel import/export changes
- Copy/Revidieren changes
- ANHANG fixture behavior changes

Evidence:

- imported row count
- FlatItem L0/L1/L2 count
- orphan count
- exported workbook parsed values
- UI screenshot/table value comparison
- build/test command output

Pass criteria:

- exported values match rendered UI
- process map export includes full folder hierarchy
- deep-copy preserves all risk columns
- no orphan FMEA rows after process sync

## safert-prozesskarte-ui-harness

Based on:

- `safert-risk-prozesskarte`
- `safert-dgmp-ui-guideline`

Use when:

- Risk Process Map visual changes
- ReactFlow diagram changes
- DGMP document overview changes

Evidence:

- desktop screenshot
- node/edge count
- console errors
- connector geometry check
- editor regression check

Pass criteria:

- zero diagonal connectors
- zero unintended overlaps
- read-only page uses document palette
- editor remains unchanged

## safert-dev-test-handoff-harness

Based on:

- `safert-dev-test-handoff`
- `safert-issue-board-sync`
- `safert-agentic-notion-workflow`

Use when:

- DEV requests TEST verification
- TEST reports pass/fail
- Notion issue status moves

Evidence:

- commit SHA
- preview URL
- DoD checklist
- TEST verified HEAD SHA
- pass/fail findings

Pass criteria:

- DEV only moves issue to Ready-for-Test
- TEST owns Done
- handoff includes SHA and what to check

## safert-dgmp-ui-review-harness

Based on:

- `safert-dgmp-ui-guideline`
- `safert-mockup-harness`
- `safert-ui-branch-gate`

Use when:

- SafeRT UI mockup or implementation needs design review
- a UI branch/preview decision is needed

Evidence:

- screenshot(s)
- affected route
- design token comparison
- brand asset check
- manual usability notes

Pass criteria:

- semantic colors only
- no decorative noise
- brand assets unchanged
- text not silently truncated where it matters
- branch strategy matches change risk

## safert-german-report-regulatory-harness

Based on:

- `safert-german-report-compliance`
- `safert-fmea-risk-domain`
- `safert-sae-sync-contract`

Use when:

- report output changes
- German compliance wording changes
- residual risk or revision evidence changes

Evidence:

- report screenshot/PDF
- data source references
- residual risk basis
- revision/signature fields

Pass criteria:

- report uses real data
- residual risk is after controls
- German clinical/regulatory wording is coherent
- missing evidence is flagged

