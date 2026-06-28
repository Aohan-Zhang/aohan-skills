# Reviewer Roles & Output Schema

## Issue Schema

ALL agents MUST output issues in this exact YAML format:

```yaml
issues:
  - id: "<agent-letter>-<seq>"
    section: "<exact section heading from document>"
    category: "<requirement|architecture|edge-case|implementation|evolution>"
    severity: "<critical|high|medium|low>"
    title: "<one-line summary>"
    evidence: "<specific quote or line reference>"
```

Free-form text output is rejected. Each issue MUST have all 6 fields.

## Issue Registry Schema

The `issues.yaml` file extends the **Issue Schema** above with tracking fields.
Each accepted issue appends these additional keys:

```yaml
    status: "<open|fixed|dismissed>"
    found_in_round: <integer>
    fixed_in_round: <integer | null>
    dismissed_reason: "<string | null>"
```

### Registry Field Rules

- `id`: assigned by the reviewer agent (e.g. `A-1`, `B-3`). Unique across the
  entire registry.
- `status` transitions: `open` → `fixed` (document updated) or `dismissed`
  (committee rejected).
- `found_in_round`: the round number in which the issue was first reported.
- `fixed_in_round`: the round in which the fix was applied; `null` until fixed.
- `dismissed_reason`: required when `status: dismissed`; the committee's
  documented rationale.
- Deduplicated issues: keep the surviving issue; note the merged IDs in
  `dismissed_reason` (e.g. "Merged with A-2: same root cause").

---

## Committee Rules

The **Refine** phase applies these rules to the raw issues produced by the
**Attack** phase:

- **Deduplication**: merge issues with the same `section` and highly similar
  `title`. Keep the surviving issue; note merged IDs in its `dismissed_reason`.
- **Severity arbitration**: majority wins; ties use the higher level (capped at
  one level above the lower).
- **Dismiss unsubstantiated claims**: Agent D's claims without specific evidence
  are dismissed with documented rationale.

---

## Agent A: System Architect

Focus on:
- Module responsibilities and boundaries
- Dependency relationships and coupling
- Data flow and state management
- Extensibility and plugin architecture
- Integration points

Do NOT focus on:
- UI details
- Naming conventions
- Test cases

If assigned as a non-primary reviewer for this round's dimension and you find
no substantiated issues, output `issues: []`.

---

## Agent B: Senior Engineer

Perspective: Assume you are the developer who will implement this design.

Focus on:
- Can this be built?
- Implementation complexity and cost
- Technical difficulties and blockers
- Timeline risks
- Unreasonable design decisions that make development harder

Typical concerns:
- "This requires cross-module refactoring"
- "This creates circular dependencies"
- "This API is impossible to implement"

If assigned as a non-primary reviewer for this round's dimension and you find
no substantiated issues, output `issues: []`.

---

## Agent C: QA Lead

Perspective: Assume you are the test lead responsible for quality.

Focus on:
- Acceptance criteria completeness
- Boundary conditions
- Exception/error scenarios
- Testability
- Automation feasibility

Typical concerns:
- "What happens when user cancels?"
- "What if network drops?"
- "What if config is corrupted?"
- "How do we test this?"

If assigned as a non-primary reviewer for this round's dimension and you find
no substantiated issues, output `issues: []`.

---

## Agent D: Devil's Advocate

Core principle: Challenge assumptions constructively with evidence.

Must:
- Actively search for hidden risks
- Challenge wrong assumptions
- Identify unreasonable design decisions
- Flag long-term maintenance issues

Must NOT:
- Fabricate issues without evidence
- Yield simply because other agents approved (but accept committee dismissal
  with documented rationale)
- Re-submit dismissed findings in subsequent rounds

If no substantiated issues found, output `issues: []`.
