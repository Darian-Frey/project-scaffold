<!--
IMPROVEMENTS.skeleton.md — copy to IMPROVEMENTS.md and fill in placeholders.
See: development_documentation.md §Per-Document Specifications → IMPROVEMENTS.md
Catalogue of code-quality improvements, refactors, and architectural changes
proposed during development.
Stable IDs (IMP-NNN) are append-only.
Status vocabulary: suggested | applied | declined | deferred.
Effort vocabulary: trivial | small | medium | large.

The dual of BUGS.md: bugs are broken; improvements work but could be better.
Distinct from FEATURES.md candidate features (user-facing capabilities) and from
DECISIONS.md proposed entries (choices between alternatives) — IMP entries are
internal-facing candidate changes that haven't yet been adjudicated.

Per Maintenance Rule 8 in the standard: improvements are logged here when noticed,
not silently applied. The author decides whether to apply, defer, or decline.
Trade-offs are required — an entry without trade-offs is a feature request,
not a candidate improvement.
-->

# Improvements

Catalogue of code-quality improvements, refactors, and architectural changes proposed during development. Per Maintenance Rule 8, improvements are logged here when noticed, not silently applied. The author decides whether to apply, defer, or decline.

This is the dual of [BUGS.md](BUGS.md): bugs are things that are *broken*; improvements are things that *work but could be better* (clarity, reuse, maintainability, performance, future flexibility).

Status vocabulary: suggested | applied | declined | deferred.
Effort vocabulary: trivial | small | medium | large.

---

## Suggested

### IMP-001 {short title}

**Status:** suggested
**Found:** YYYY-MM-DD ({session/commit context})
**Location:** {path/to/file.ext:line, or "cross-cutting"}
**Effort:** {trivial | small | medium | large}
**Description.** {What could be improved and why.}
**Proposal.** {How to do it. Concrete enough that the user can decide without re-deriving the plan.}
**Trade-offs.** {What we'd give up or risk. Required — without this the entry is a feature request, not a candidate improvement.}
**Notes.** {Related context, dependencies on other work, links to BUG/IMP/D-NNN entries.}

---

## Applied

### IMP-002 {short title}

**Status:** applied (YYYY-MM-DD)
**Location:** {path/to/file.ext:line — files actually touched}
**Effort:** {what it actually was, not what was estimated}
**Description.** {The improvement, in retrospect.}
**Change.** {What was done; reference the commit if useful.}
**Trade-offs.** {What we gave up. Keep this honest — if the trade-offs turned out worse than expected, that's signal for future IMPs.}
**Notes.** {Follow-ups, cross-references.}

---

## Declined

{Entries with `Status: declined`. Keep for audit trail — explain why the candidate was rejected. A future maintainer revisiting the same idea should be able to find the prior reasoning.}

---

## Deferred

{Entries with `Status: deferred`. Distinct from declined: deferred means "intend to apply later", declined means "decided against".}
