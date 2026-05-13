<!--
ATTACK_VECTORS.skeleton.md — copy to ATTACK_VECTORS.md and fill in placeholders.
See: development_documentation.md §Per-Document Specifications → ATTACK_VECTORS.md
Project-specific failure modes with detection methods.
Stable IDs (AV-NNN) are append-only.
Severity vocabulary: Critical (must hold) | Major (regression on release blocks) | Minor (track only).

Distinct from TESTING.md (which describes test infrastructure) and SECURITY.md (which is adversarial threats only).
Detection is not optional — a vector without a detection method is a worry, not a vector.
-->

# Attack Vectors

Project-specific failure modes the project must be resilient against.

Grouped by category. Each vector lists detection method and severity.

Severity: Critical (must hold) | Major (regression on release blocks) | Minor (track only).

---

## {Category — e.g. Physics validity, Numerical stability, Performance, Correctness, Security}

### AV-001 {Vector title}

**Severity:** {Critical | Major | Minor}
**Description.** {What can go wrong. The specific failure mode, stated precisely.}
**Detection.** {How it is checked — test path, tool, manual review, audit step. Required.}
**Related decisions.** D-NNN
**Related claims.** C-NNN  <!-- if applicable -->
**History.** {When/how this vector was identified, prior incidents, any tightening of bounds.}

### AV-002 {Vector title}

**Severity:** Major
**Description.** {What can go wrong.}
**Detection.** {How it is checked.}
**Related decisions.** D-NNN

## {Next category}

### AV-003 {Vector title}

**Severity:** Critical
**Description.** {What can go wrong.}
**Detection.** {How it is checked.}
**Related decisions.** D-NNN
