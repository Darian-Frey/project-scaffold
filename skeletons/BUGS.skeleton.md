<!--
BUGS.skeleton.md — copy to BUGS.md and fill in placeholders.
See: development_documentation.md §Per-Document Specifications → BUGS.md
Catalogue of bugs discovered during development.
Stable IDs (BUG-NNN) are append-only.
Status vocabulary: open | fixed | wontfix | deferred.
Severity vocabulary: low | medium | high.

Distinct from ATTACK_VECTORS.md (forward-looking checklist of anticipated failure modes).
BUGS is the backward-looking log of what actually went wrong, with status flags.

Per Maintenance Rule 8 in the standard: bugs are logged here when found,
not silently fixed. The author decides whether to fix immediately, defer,
or leave alone. Reproduction is required for open bugs.
-->

# Bugs

Catalogue of bugs discovered during development. Per Maintenance Rule 8, bugs are logged here when found, not silently fixed. The author decides whether to fix immediately, defer, or leave alone.

Status vocabulary: open | fixed | wontfix | deferred.
Severity vocabulary: low | medium | high.

---

## Open

### BUG-001 {short title}

**Status:** open
**Found:** YYYY-MM-DD ({session/commit context})
**Location:** {path/to/file.ext:line, or "cross-cutting"}
**Severity:** {low | medium | high}
**Description.** {What's wrong and why it matters.}
**Reproduction.** {Minimum steps to trigger. Required for open bugs — if not yet isolated, say so explicitly rather than leaving blank.}
**Notes.** {Related context, suggested fix, links to BUG/IMP/D-NNN/AV entries.}

---

## Fixed

### BUG-002 {short title}

**Status:** fixed (YYYY-MM-DD)
**Found:** YYYY-MM-DD ({session/commit context})
**Location:** {path/to/file.ext:line}
**Severity:** {low | medium | high}
**Description.** {What was wrong.}
**Reproduction (was).** {How it could be triggered before the fix.}
**Fix.** {What changed; reference the commit if useful.}
**Notes.** {Cross-references, lessons learned.}

---

## Won't Fix

{Entries with `Status: wontfix`. Keep for audit trail — explain why the bug was left unfixed.}

---

## Deferred

{Entries with `Status: deferred`. Distinct from wontfix: deferred means "intend to fix later", wontfix means "decided not to fix".}
