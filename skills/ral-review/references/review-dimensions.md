# Review Dimensions by Round

## Round-Agent Matrix

Each agent participates in all rounds but adjusts focus per the matrix below.

| Round | Dimension | Agent A (Architect) | Agent B (Engineer) | Agent C (QA) | Agent D (Devil's Advocate) |
|-------|-----------|---------------------|-------------------|--------------|---------------------------|
| R1 | Requirements | Check requirement-architecture alignment | Assess feasibility of requirements | Validate acceptance criteria completeness | Challenge assumptions in requirements |
| R2 | Architecture | Primary reviewer | Identify implementation blockers | Check testability of architecture | Attack coupling and dependencies |
| R3 | Edge Cases | Review system-level failure modes | Assess error handling complexity | Primary reviewer | Challenge error recovery assumptions |
| R4 | Implementation | Validate architectural integrity | Primary reviewer | Verify test coverage plan | Attack implementation shortcuts |
| R5 | Future Evolution | Primary reviewer | Assess technical debt | Check maintainability | Challenge extensibility claims |

## Round 1: Requirement Completeness Review

Check for:
- Requirement gaps
- User scenario gaps
- Business rule gaps
- Acceptance criteria gaps
- Stakeholder alignment
- Success metrics

Output: Issues, Risks, Missing Information

---

## Round 2: Architecture Review

Check for:
- Module responsibilities
- Data flow clarity
- State management approach
- Extensibility design
- Coupling and dependencies
- Technology choices

Output: Architecture Issues, Architecture Risks, Refactoring Suggestions

---

## Round 3: Edge Case Review

Check for:
- Exception flows
- Extreme inputs
- Concurrency issues
- Failure handling
- Boundary conditions
- Error recovery

Output: Edge Case Issues, Failure Scenarios, Recovery Mechanisms

---

## Round 4: Implementation Review

Check for:
- Implementation complexity
- Development cost estimate
- Technical difficulty
- Timeline feasibility
- Unreasonable design
- Blockers and dependencies

Output: Implementation Issues, Complexity Concerns, Technical Risks

---

## Round 5: Future Evolution Review

Check for:
- Long-term maintainability
- Plugin/extension capability
- Scalability path
- Technical debt risk
- Migration strategy
- Backward compatibility

Output: Evolution Issues, Extensibility Gaps, Maintenance Risks
