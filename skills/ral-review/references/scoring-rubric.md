# Scoring Rubric

## Maturity Score Calculation

Base score: 100

### Step 1: Base Deductions

Deductions per unique issue (count each issue ONCE, exclude `status: dismissed`):

| Severity | Deduction |
|----------|-----------|
| Critical | -25 |
| High | -15 |
| Medium | -8 |
| Low | -3 |

### Step 2: Clustering Multiplier

Issues are "related" if they share the same `section` AND same `category`. Apply multiplier to the cluster's total deduction:

- 1 isolated issue: 1.0x
- 2-3 related issues in same section+category: 1.2x
- 4+ related issues in same section+category: 1.5x (systemic problem)

### Step 3: Round Adjustments

- Each FULL round (4 agents) with zero new issues: +2 bonus
- Partial rounds (< 4 agents) receive NO bonus regardless of issue count
- Maximum bonus: +10 total across all rounds

### Step 4: Late Discovery Penalty

- Each Critical issue found in Round 4 or 5: additional -5 penalty
- "After Round 3" = Round 4 and Round 5 only (not inclusive of Round 3)

### Step 5: Final Score

```
score = base(100) - sum(deductions × clustering_multiplier) + round_bonuses - late_penalties
```

Score capped at 100 (cannot exceed base).
Score cannot go below 0.

## Per-Dimension Breakdown

Each dimension's INTRINSIC score (before weight):

```
dimension_score = 100 - total_deductions_for_issues_in_this_dimension
```

Weight is applied ONLY to the overall score contribution, NOT to the dimension's own score:

| Dimension | Rounds | Weight in Overall Score |
|-----------|--------|------------------------|
| Requirements | R1 | 25% |
| Architecture | R2 | 25% |
| Edge Cases | R3 | 20% |
| Implementation | R4 | 20% |
| Future Evolution | R5 | 10% |

Example: Edge Cases dimension has 30 points of deductions → dimension score = 70 (identifies as weak). Its contribution to overall score = 30 × 0.20 = 6 points deducted from overall.

The final report lists each dimension's intrinsic score (0-100) to identify the weakest area.

## Severity Definitions

### Critical

- Blocks implementation entirely
- Causes data loss or corruption
- Creates security vulnerability
- Makes the design fundamentally unsound

Example: "API has no authentication mechanism"

### High

- Significantly impacts quality or maintainability
- Creates major technical debt
- Will require major refactoring to fix later
- Affects core user workflows

Example: "No error handling for network failures"

### Medium

- Noticeable gap in requirements or design
- Should be addressed before implementation
- Creates friction for developers or users
- Missing edge case coverage

Example: "Unclear behavior when user cancels mid-operation"

### Low

- Minor improvement opportunity
- Style or consistency issue
- Nice-to-have enhancement
- Documentation gap

Example: "Variable naming could be more descriptive"

## Agent Ready Verdict

- **YES**: Score ≥ 80 AND zero Critical/High unresolved issues
- **NO**: Score < 80 OR any Critical/High issue unresolved

When verdict is NO, report must include:
1. Specific sections needing improvement
2. Weakest dimension (lowest intrinsic dimension score)
3. Whether all 5 dimensions were reviewed
4. Recommended next steps
