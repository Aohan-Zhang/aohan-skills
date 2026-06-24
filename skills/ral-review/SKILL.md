---
name: ral-review
description: Design document review using RAL (Review → Attack → Refine). Use when reviewing, auditing, or improving a design spec, PRD, architecture doc, or API design before implementation.
---

# RAL Review (Review → Attack → Refine)

Iterative design document review using Review → Attack → Refine cycles. Spawn 4
reviewer subagents across 5 dimensions to bring a design doc to "Agent Ready"
quality: unambiguous, complete, and directly implementable.

## Execution Modes

- `auto` (default): Run up to 5 rounds, apply accepted fixes directly to the
  document, and produce a scored maturity report.
- `dry`: Run the review but do not modify the document. Output issues and
  reports only.
- `quick`: Run only Round 1 (Requirement Completeness) and output a concise
  issue list. No scoring or auto-fix.

If no mode is given, use `auto`.

## Workflow

1. **Initialize**
   - Validate input: file exists and is readable.
   - Create `<document-dir>/.ral-review/<timestamp>/`.
   - Save original as `round-0.md`.
   - Initialize `issues.yaml`.
   - Decide rounds: `quick` → 1 round; `auto` / `dry` → up to 5 rounds.

2. **Per-round loop** (Round 1..N)
   - **Snapshot** current document as `round-{N}.md`.
   - **Context injection**: give each reviewer the current dimension, prior
     issues, and sections modified so far.
   - **Independent review**: spawn the 4 reviewer subagents in parallel. Each
     returns structured issues with: `id`, `section`, `category`, `severity`,
     `title`, `evidence`.
   - **Committee discussion**:
     - Deduplicate issues with the same `section` and highly similar `title`.
     - Arbitrate severity: majority wins; ties use the higher level (capped at
       one level above the lower).
     - Dismiss unsubstantiated claims from Agent D with documented rationale.
   - **Update registry**: append accepted issues to `issues.yaml` with
     `status: open` and `found_in_round`.
   - **Document update** (`auto` only): edit the target document to fix accepted
     issues. Preserve headings, do not add TODOs, append new sections under the
     relevant parent. On failure, roll back to `round-{N}.md` and reopen that
     round's issues.
   - **Report**: output new issues, fixed issues, dismissed issues, remaining
     risks, and modified sections.

3. **Stop when**
   - 2 consecutive full rounds produce no new Medium+ issues, or
   - 5 rounds completed, or
   - `quick` mode Round 1 finished.

   Exception: a Critical issue in `auto`/`dry` allows one extra round beyond the
   normal stop condition.

4. **Finalize**
   - `auto`: generate the maturity report using
     `references/scoring-rubric.md`.
   - `dry`: generate a report of all found issues and proposed fixes.
   - `quick`: generate a concise Round 1 issue list.

## Reviewer Roles

See `references/reviewer-roles.md` for full prompts.

- **Agent A — System Architect**: modules, dependencies, data flow,
  extensibility.
- **Agent B — Senior Engineer**: implementability, cost, technical risk,
  timeline.
- **Agent C — QA Lead**: acceptance criteria, edge cases, testability.
- **Agent D — Devil's Advocate**: challenges assumptions, finds hidden risks.

## Review Dimensions by Round

See `references/review-dimensions.md` for detailed checklists.

| Round | Dimension |
|-------|-----------|
| 1 | Requirement Completeness |
| 2 | Architecture Review |
| 3 | Edge Case Review |
| 4 | Implementation Review |
| 5 | Future Evolution Review |

## Severity Levels

- **Critical**: blocks implementation, data loss, security vulnerability.
- **High**: significantly impacts quality, maintainability, or core workflows.
- **Medium**: noticeable gap that should be fixed before implementation.
- **Low**: minor improvement, style, or nice-to-have.

## Final Report

`auto` mode must output:

1. Total unique issues found
2. Issues per round and per dimension
3. Issues fixed / dismissed
4. Remaining risks
5. Maturity score (0–100) from `references/scoring-rubric.md`
6. **Agent Ready verdict**: YES if score ≥ 80 and zero unresolved Critical/High
   issues, otherwise NO.

`dry` / `quick` modes output a concise report without scoring.

## Usage

```
/ral-review <path-to-document> [mode]
```

Examples:

```
/ral-review docs/specs/payment-system.md
/ral-review docs/specs/payment-system.md dry
/ral-review docs/specs/payment-system.md quick
```
