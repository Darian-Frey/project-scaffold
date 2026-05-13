<!--
DECISIONS.skeleton.md — copy to DECISIONS.md and fill in placeholders.
See: development_documentation.md §Per-Document Specifications → DECISIONS.md
Append-only log of significant design decisions with rationale and reversal conditions.
Stable IDs (D-NNN) are sequential and never reused.
Status vocabulary: Proposed | Accepted | Superseded by D-NNN | Deprecated.

Date fields:
- "Decided:" is when the choice was actually made.
- "Recorded:" is when the entry was written.
- Same date for normal entries. For retroactive entries (e.g. during retroactive completion),
  the two diverge — set Decided to the original date if recoverable (e.g. from a commit),
  or omit Decided and annotate if the original date is lost.

Maintenance rules:
- Append-only. Reversed decisions get a new entry; old entry status becomes "Superseded by D-NNN".
- One decision per entry.
- Reversal conditions are not optional — a decision without one is a belief, not a decision.
-->

# Decisions

Append-only log of significant design decisions for {project name}.

Each entry: D-NNN, with Decided and Recorded dates (ISO 8601), status, context, options, decision, consequences, and reversal conditions.

Status vocabulary: Proposed | Accepted | Superseded by D-NNN | Deprecated.

---

### D-001 {Decision title}

**Decided:** YYYY-MM-DD
**Recorded:** YYYY-MM-DD
**Status:** {Proposed | Accepted | Superseded by D-NNN | Deprecated}
**Authors:** {author} (with {critic tool} review {date} if applicable)
**Related:** F-NNN, C-NNN, AV-NNN

**Context.** {Why this decision was needed. The problem being addressed; constraints; what existed before.}

**Options.**

- **A. {Option name}.** {Brief description. Why considered, why rejected or chosen.}
- **B. {Option name}.** {Brief description. Why considered, why rejected or chosen.}
- **C. {Option name}.** {Brief description. Chosen.}

**Decision.** {Chosen option, restated. The decision itself, stated cleanly.}

**Consequences.**

- {Implication of this choice — what becomes possible, what becomes harder, what cost is incurred.}
- {Implication.}

**Reversal conditions.** {What evidence would change this decision. Specific enough that you'd recognise the trigger when it occurred — not "if it stops working" but "if measured X exceeds Y on platform Z".}
