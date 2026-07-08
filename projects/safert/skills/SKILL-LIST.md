# SafeRT Skill List

This is the shared SafeRT vocabulary for Hermes agents.

When the USER names one of these skills, agents should understand the intended
review lens, source documents, and expected output.

## 1. safert-agent-rules

- Korean alias: 세이프알티 에이전트 규칙
- Use when: an agent starts work in the SafeRT repository, or when behavior is unclear.
- Primary agents: DEV, SMARTIE, TEST, SENSI, STEIN
- Source docs: `CLAUDE.md`, `AGENTS.md`, `docs/COLLABORATION_WORKFLOW.md`, Notion Dev Wiki agent guide.
- What agents should do: follow SafeRT repo commands, FSD boundaries, issue completion rules, Notion issue sync, branch strategy, and author-vs-approver separation.
- Output expected: concise plan or compliance check against SafeRT agent rules.

## 2. safert-prd

- Korean alias: 세이프알티 PRD
- Use when: judging product intent, feature scope, or whether a change matches the product.
- Primary agents: SMARTIE, MAX, DEV, SENSI
- Source docs: `docs/PRD.md`, Notion SafeRT Dev Wiki roadmap.
- What agents should do: compare proposal/code against SafeRT FMEA product requirements: FMEA table, process mapping, risk assessment, AI, export/report, localization.
- Output expected: product-fit judgment, missing requirements, requirement updates.

## 3. safert-architecture-fsd

- Korean alias: 세이프알티 아키텍처
- Use when: adding modules, moving code, or reviewing implementation structure.
- Primary agents: DEV, SENSI, SMARTIE
- Source docs: `docs/ARCHITECTURE.md`, `CLAUDE.md`, `AGENTS.md`.
- What agents should do: preserve Feature-Sliced Design layers, React/Zustand/TanStack boundaries, entity/feature/shared separation.
- Output expected: file placement guidance, architecture risk, refactor constraints.

## 4. safert-fmea-risk-domain

- Korean alias: FMEA 위험 도메인
- Use when: checking risk-table behavior, FMEA terminology, or risk calculation meaning.
- Primary agents: STEIN, SMARTIE, DEV, TEST
- Source docs: `docs/PRD.md`, `mockups/glossary-rt-fmea.md`, FMEA Excel fixtures.
- What agents should do: apply RPN, Risk Matrix, AP, Task Priority, Existing/Planned Measures, German FMEA vocabulary.
- Output expected: domain correctness review and risk-method implications.

## 5. safert-sae-sync-contract

- Korean alias: SAE 동기화 계약
- Use when: any S/A/E, S/O/D, risk method, import, or measure update changes.
- Primary agents: DEV, STEIN, TEST, SENSI
- Source docs: `docs/ADR-001-SAE-synchronization.md`, `docs/ADR-002-measure-changes-risk-reset.md`, `CLAUDE.md`.
- What agents should do: enforce one shared Severity/Occurrence/Detection reality across all methods; detect conflict/reset risks.
- Output expected: sync impact list, affected views, required warnings/tests.

## 6. safert-process-map-sot

- Korean alias: 공정맵 단일진실원장
- Use when: process hierarchy, FlatItem, FMEA row linkage, import sync, or process columns are involved.
- Primary agents: DEV, TEST, STEIN
- Source docs: `docs/ADR-003-process-fmea-sync.md`, `docs/ADR-005-fmea-import-process-hierarchy-sot.md`.
- What agents should do: treat Process Map FlatItem hierarchy as the source of truth for Main/Sub Process rendering and row linkage.
- Output expected: linkage contract, orphan risk, idempotency/test requirements.

## 7. safert-excel-fidelity

- Korean alias: 엑셀 입출력 충실도
- Use when: Excel import/export, WYSIWYG export, copy/revidieren, or ANHANG fixtures are touched.
- Primary agents: DEV, TEST, SENSI
- Source docs: `docs/ADR-004-import-export-behavior.md`, `docs/ADR-007-excel-export-and-deep-copy-fidelity.md`, Excel fixtures.
- What agents should do: verify export mirrors UI-rendered values, process map export enumerates folder hierarchy, deep-copy preserves all columns.
- Output expected: import/export fidelity checklist and required fixture tests.

## 8. safert-dgmp-ui-guideline

- Korean alias: DGMP UI 가이드
- Use when: creating or reviewing SafeRT UI, especially medical/German document surfaces.
- Primary agents: SENSI, KKUMI, DEV, TEST, STEIN
- Source docs: `docs/UI_DESIGN_GUIDELINES.md`, `docs/UI_GUIDE.md`, Notion Germany design pages.
- What agents should do: enforce clean, calm, printable medical quality-management style; semantic colors; no decorative noise; fixed brand assets.
- Output expected: UI critique, token check, screenshot-verifiable recommendations.

## 9. safert-risk-prozesskarte

- Korean alias: 리스크 프로세스카르테
- Use when: Risk Process Map, DGMP Prozesskarte, ReactFlow diagram, hazards, measures, connectors, or read-only overview changes.
- Primary agents: DEV, TEST, SENSI, STEIN
- Source docs: `docs/ADR-006-risk-process-map-prozesskarte.md`, `docs/UI_DESIGN_GUIDELINES.md`.
- What agents should do: preserve readOnly/individualFms gating, orthogonal connectors, one FM hexagon to one measure, no editor regression.
- Output expected: diagram implementation/review checklist and visual verification criteria.

## 10. safert-hospital-tenancy

- Korean alias: 병원 테넌시
- Use when: hospital, department, treatment room, protocol, role, credential URL, or membership flows change.
- Primary agents: SMARTIE, SENSI, DEV, TEST
- Source docs: `docs/REQ-HOSP-LIFECYCLE-ROLE-UI-DESIGN.md`, `docs/REQ-HOSP-TREATMENT-ROOM-CRUD-DESIGN.md`, `docs/DEV-HOSPITAL-PHASE1-FINAL-SPEC-2026-06-30.md`, Notion hospital mockup pages.
- What agents should do: apply hospital/protocol hierarchy, role boundaries, membership/no-access states, admin/read-only behavior.
- Output expected: product flow review, data model impact, UX states.

## 11. safert-german-report-compliance

- Korean alias: 독일 보고서 컴플라이언스
- Use when: German report, PDF/export report, signature/history/residual risk, or regulatory wording changes.
- Primary agents: STEIN, DEV, TEST, SMARTIE
- Source docs: Notion Dev Wiki Report roadmap, `docs/PRD.md`, report mockups, `SafeRT_MPE_평가보고서.md`.
- What agents should do: check German-ready report structure, real data, revision history, residual risk after controls, references such as StrlSchV / ISO 14971 / DGMP where applicable.
- Output expected: compliance-oriented report checklist and gaps.

## 12. safert-ai-jury-consensus

- Korean alias: AI 배심원 합의
- Use when: AI model comparison, multi-model review, jury scoring, or consensus UX is involved.
- Primary agents: SMARTIE, SENSI, MAX, STEIN
- Source docs: `docs/REQ-AI-JURY-CONSENSUS-DESIGN.md`, `docs/SENSI-AI-JURY-CONSENSUS-UX-HANDOFF-2026-07-02.md`, Notion AI tuning pages.
- What agents should do: structure multi-model disagreement, scoring, consensus synthesis, and human-in-the-loop decision display.
- Output expected: jury workflow, scoring dimensions, UX risks.

## 13. safert-agent-rag-citation

- Korean alias: 에이전트 RAG 인용
- Use when: SafeRT Agent 4.1, RAG corpus, citations, retrieval, or answer grounding changes.
- Primary agents: SMARTIE, DEV, STEIN, SENSI
- Source docs: `docs/agent-4.1/README.md`, `docs/agent-4.1/v1.1-system-prompt.txt`, `docs/agent-4.1/rag-corpus-v1_1.json`, `docs/FMEA-RAG-ENHANCED-v10-WORKORDER.md`.
- What agents should do: preserve grounded answers, citation hardening, retrieval routing, and domain-safe responses.
- Output expected: citation/retrieval checklist and hallucination risk review.

## 14. safert-agentic-notion-workflow

- Korean alias: 세이프알티 노션 협업
- Use when: Notion communication, issue board, queue, watcher, archive, or multi-PC collaboration is involved.
- Primary agents: SMARTIE, DEV, TEST, SENSI
- Source docs: `tools/notion/README.md`, `tools/notion/CHANNELS.md`, `docs/NOTION-WATCH-EXTENSION-PROMPT.md`, Notion Dev Wiki agent guide.
- What agents should do: keep channel-local replies, use queue/inbox semantics, respect Notion rate limits, archive safely, avoid watcher duplication.
- Output expected: messaging route, queue state, operational risk.

## 15. safert-dev-test-handoff

- Korean alias: 개발-테스트 핸드오프
- Use when: DEV hands work to TEST, TEST reports verification, or a commit needs acceptance.
- Primary agents: DEV, TEST, SMARTIE
- Source docs: `docs/COLLABORATION_WORKFLOW.md`, `CLAUDE.md`, `AGENTS.md`.
- What agents should do: hand off task/SHA/preview/DoD; TEST confirms HEAD; author does not self-approve Done.
- Output expected: one-line handoff or verification verdict.

## 16. safert-ui-branch-gate

- Korean alias: UI 브랜치 게이트
- Use when: deciding whether a UI change should go straight to shared branch or separate `ui/<topic>` worktree/preview.
- Primary agents: SENSI, DEV, TEST, SMARTIE
- Source docs: `CLAUDE.md`, `AGENTS.md`, `docs/SENSI-4-CYCLE-DESIGN-CADENCE-2026-07-02.md`.
- What agents should do: apply the one-hour broken-state rule, 5174 vs 5175 preview split, manual UI regression checklist.
- Output expected: branch strategy decision and merge gates.

## 17. safert-mockup-harness

- Korean alias: 목업 하네스
- Use when: using or creating SafeRT mockups, screenshots, presentation assets, or design exploration.
- Primary agents: SENSI, KKUMI, SMARTIE, MAX
- Source docs: `mockups/README.md`, `mockups/PLAN.md`, `mockups/PLAN-REGISTRY.md`, Notion v2/planning pages.
- What agents should do: find relevant mockups, compare variants, keep screenshot evidence, connect mockup to PRD/issue/implementation handoff.
- Output expected: mockup source list, chosen direction, implementation notes.

## 18. safert-beta-pilot-evidence

- Korean alias: 베타 파일럿 근거
- Use when: user pilot, survey, acceptance, or real-user evidence is needed.
- Primary agents: SMARTIE, MAX, SENSI
- Source docs: `docs/BETA-PILOT-USER-GUIDE-2026-07-06.md`, `docs/BETA-PILOT-SURVEY-2026-07-06.md`.
- What agents should do: convert feedback into product evidence, feature gaps, onboarding issues, and validation criteria.
- Output expected: user-evidence summary and product implications.

## 19. safert-security-deploy

- Korean alias: 배포 보안
- Use when: deployment, install package, security plan, environment setup, or server operation is involved.
- Primary agents: DEV, TEST, STEIN
- Source docs: `INSTALL.md`, `HANDOFF.md`, `mockups/11-deploy-security/DEPLOY-SECURITY-PLAN.md`, `mockups/11-deploy-security/INSTALL-GUIDE.md`.
- What agents should do: preserve secure deployment assumptions, environment variables, install flow, and operational checks.
- Output expected: deploy checklist, risk notes, install verification.

## 20. safert-issue-board-sync

- Korean alias: 이슈보드 동기화
- Use when: completing issues, commit messages, Notion board status, or pre-push hook behavior is involved.
- Primary agents: DEV, SMARTIE, TEST
- Source docs: `CLAUDE.md`, `AGENTS.md`, `tools/notion/sync-board.mjs`, `tools/notion/issue.mjs`.
- What agents should do: use `Closes <ID>` only on final slice; DEV moves to Ready-for-Test; TEST moves to Done.
- Output expected: correct issue status transition plan.

## Quick Use

```text
safert-dgmp-ui-guideline으로 이 목업 봐줘.
safert-sae-sync-contract 기준으로 이 변경 위험 봐줘.
safert-excel-fidelity 돌려서 export 깨질지 봐줘.
safert-dev-test-handoff 형식으로 개발이에서 투덜이에게 넘겨줘.
```

