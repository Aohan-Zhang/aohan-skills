---
name: ral-review
description: Design document review using RAL (Review → Attack → Refine) cycles.
disable-model-invocation: true
---

# RAL Review (Review → Attack → Refine)

Iterative design document review using Review → Attack → Refine cycles. Spawn 4
reviewer subagents across 5 dimensions to bring a design doc to **Agent Ready**
quality: unambiguous, complete, and directly implementable.

**Agent Ready** is the target state — every round pushes toward it, and the
final verdict declares whether the document has reached it.

## Execution Modes

| Mode | Rounds | Modifies doc | Output |
|------|--------|-------------|--------|
| `quick` (default) | 1 | Yes | Concise issue list |
| `auto` | Up to 5 | Yes | Scored maturity report |
| `dry` | Up to 5 | No | Issues and proposed fixes |

If no mode is given, use `quick`.

## Working Directory

All working artifacts (snapshots, issue registry) are written to the **system
temporary directory**:

- Linux / macOS: `/tmp/ral-review/<doc-name>/<timestamp>/`
- Windows: `%TEMP%\ral-review\<doc-name>\<timestamp>/`

`<doc-name>` is the reviewed file's stem (e.g. `payment-system` from
`payment-system.md`). This keeps artifacts out of the source tree and avoids
polluting git-tracked directories.

## Workflow

1. **Initialize**
   - Create working directory under system temp:
     `<tmp>/ral-review/<doc-name>/<timestamp>/`.
   - Save original as `round-0.md` in the working directory.
   - Initialize `issues.yaml` in the working directory (schema in
     `references/reviewer-roles.md`).
   - `auto` and `quick` modes only: create a backup copy of the original
     document at `<document-path>.backup` (e.g. `payment-system.md.backup`).
     Inform the user: "A backup has been created at `<document-path>.backup`.
     Delete it manually once you are satisfied with the changes."
   - Decide rounds: `quick` → 1 round; `auto` / `dry` → up to 5 rounds.

   **Done when:** `round-0.md` and `issues.yaml` exist in working directory;
   backup created (if applicable); round count set.

2. **Per-round loop** (Round 1..N)
   - **Snapshot** current document as `round-{N}.md` in the working directory.
   - **Context injection**: give each reviewer the current dimension, prior
     issues, and sections modified so far.
   - **Attack**: spawn the 4 reviewer subagents (see
     `references/reviewer-roles.md`). Each returns structured issues following
     the output schema defined there.
   - **Refine** (committee discussion — rules in
     `references/reviewer-roles.md` → Committee Rules):
     - Deduplicate, arbitrate severity, dismiss unsubstantiated claims.
     - Append accepted issues to `issues.yaml` with `status: open` and
       `found_in_round`.
   - **Document update** (`auto` and `quick` modes): edit the target document
     to fix accepted issues. Do not add TODOs; append new sections under the
     relevant parent. On failure, roll back to `round-{N}.md` and reopen that
     round's issues.
   - **Report**: output new issues, fixed issues, dismissed issues, remaining
     risks, and modified sections.

   **Done when:** every issue this round has a `status` transition in
   `issues.yaml`; document edited (if applicable); round report output.

3. **Stop when**
   - 2 consecutive full rounds (all 4 agents participated) produce no new
     Medium+ issues, or
   - 5 rounds completed, or
   - `quick` mode Round 1 finished.

   Exception: a Critical issue found in `auto`/`dry` MUST trigger one extra
   round beyond the normal stop condition.

4. **Finalize**
   - `auto`: generate the maturity report using
     `references/scoring-rubric.md`.
   - `dry`: generate a report of all found issues and proposed fixes.
   - `quick`: generate a concise Round 1 issue list.

   **Done when:** final report output containing all required fields for the
   active mode (see Final Report section).

## Review Dimensions by Round

See `references/review-dimensions.md` for detailed checklists and the
round-agent matrix.

## Severity Levels

See `references/scoring-rubric.md` → "Severity Definitions" for the
authoritative definitions of Critical, High, Medium, and Low.

## Final Report

`auto` mode must output:

1. Total unique issues found
2. Issues per round and per dimension
3. Issues fixed / dismissed
4. Remaining risks
5. Maturity score (0–100) from `references/scoring-rubric.md`
6. **Agent Ready** verdict: YES if score ≥ 80 and zero unresolved Critical/High
   issues, otherwise NO.

`dry` / `quick` modes output a concise report without scoring.

## Usage

```
/ral-review <path-to-document> [mode]
```
