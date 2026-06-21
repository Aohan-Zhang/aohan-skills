---
name: whole-codebase-search
description: >-
  Use when searching, locating, or exploring code in a codebase — finding where
  something is defined or used, tracing how a feature works, or mapping
  relationships between modules. Bias toward whole-codebase, comprehensive
  search: sweep the entire repo rather than stopping at the first match or a
  single file, and search across multiple dimensions (callers, callees, sibling
  modules, adjacent features, data flow, architectural boundaries) so nothing
  relevant is missed.
---

Default to whole-codebase, comprehensive search. The failure mode to avoid: stopping at the first match, reading a single file, or answering from the first plausible hit — and missing relevant code elsewhere in the repo.

Sweep broadly and check multiple dimensions so the picture is complete:

1. **Callers** — everything that invokes the target (functions, endpoints, handlers, event subscribers), across the whole repo.
2. **Callees** — everything the target depends on.
3. **Sibling modules** — peers in the same layer/namespace doing related work.
4. **Adjacent features** — features that touch the same data, event, or user flow.
5. **Data flow** — where data originates, is stored, and is mutated (schemas, migrations, queues, state).
6. **Architectural boundaries** — which layer owns the code and what crosses boundaries.

Prefer repo-wide tools (ripgrep over the whole repo, LSP find-references) over reading individual files. Keep searching until results stabilize — repeated queries return nothing new — not until the first hit.

Report what exists across the codebase, grouped by the dimensions above; cite `file:line`; note dimensions where nothing was found.
