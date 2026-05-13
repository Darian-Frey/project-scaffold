# Decisions

Append-only log of significant design decisions for the project-scaffold repo.

Each entry: `D-NNN`, dated ISO 8601, with status, context, options, decision, consequences, and reversal conditions.

Status vocabulary: Proposed | Accepted | Superseded by D-NNN | Deprecated.

---

### D-001 Standard format: tiered documents, stable IDs, lifecycle vocabulary

**Date:** 2026-05-13
**Status:** Accepted
**Authors:** Shane Hartley; Claude (multiple sessions, 2026-05-07 to 2026-05-12)
**Related:** `development_documentation.md` (the standard itself)

**Context.** The development documentation standard needs a structural backbone that (a) gives projects a predictable shape across language and domain, (b) lets tooling (critic tools, AI development partners) parse projects mechanically, and (c) survives multi-month gaps in attention without ambiguity about project state. Several backbone shapes were considered before settling on the current one.

**Options.**

- **A. Single monolithic README per project, expanded with sections as needed.** Simplest. Rejected: collapses orthogonal concerns (vision, features, decisions, failure modes) into one file; no stable IDs to reference from commits or reviews; no separation of current state from history.

- **B. Flat list of recommended documents with no tier structure.** Considered. Rejected: every project would face the same all-or-nothing adoption decision, with no guidance on which documents matter most. Friction would drive partial adoption with no convention for which parts to keep.

- **C. Tiered system (Tier 1 always, Tier 2 strongly recommended, Tier 3 conditional) with stable IDs (`F-NNN`, `C-NNN`, `D-NNN`, `AV-NNN`), fixed status vocabularies, and explicit lifecycle transitions.** Chosen.

**Decision.** Option C. The standard prescribes:

- **Three tiers** of documents, with Tier 1 mandatory and Tiers 2–3 added on triggers articulated in the Quick Decision Guide.
- **Stable, append-only IDs** for features, claims, decisions, and attack vectors, so commits, reviews, and external references (papers, issues) can point at specific entries that won't be renumbered.
- **Fixed status vocabularies** (project status: Active / Dormant / Complete / Archived / Superseded; decision status: Proposed / Accepted / Superseded / Deprecated; claim status: Proposed / Supported / Refuted / Withdrawn) so tooling can parse without ambiguity.
- **Project lifecycle transitions** (Active ↔ Dormant, Active → Complete, etc.) with explicit checklists, so status changes leave an audit trail rather than drifting silently.
- **Dual-audience framing**: every convention chosen serves both humans (readable prose with structure) and tooling (stable IDs, fixed vocabularies, known schema).

**Consequences.**

- Projects following the standard pay a small up-front cost (more files, more discipline) for a large compound benefit (six-month gaps become navigable; AI partners and critic tools get structured input; cross-project references are stable).
- Backward compatibility is preserved by the append-only ID rule: future revisions of the standard may add new document types but will not remove or renumber existing ones. `D-007` in any project always means the same entry it did when written.
- The standard itself is subject to its own rules. Material revisions are logged inline in the Provenance line of this repo's README header; if revision activity grows beyond inline notes, this `DECISIONS.md` becomes the authoritative log.
- Adoption is graduated, not all-or-nothing. The cost note and Quick Decision Guide explicitly support partial application based on the friction test (add a document only when its absence is currently causing confusion).

**Reversal conditions.** Revisit if any of the following hold:

- A user (or several users) report that the tier structure creates more friction than the convention saves — i.e. that the cost of Tier 1 exceeds the benefit on a meaningful class of projects.
- Tooling consuming the standard (Crucible, Cairn, Claude Code workflows) finds the schema insufficient for its needs and proposes structural additions that don't fit the current model.
- A material gap emerges that the current document set can't address — comparable to how the original draft missed `FEATURES.md` and the second revision missed `DECISIONS.md` / `ATTACK_VECTORS.md` / formal `CLAIMS.md`. Such a gap would warrant a new tier-classified document, logged as a separate decision.

If a reversal is triggered, the response is a new `D-NNN` entry proposing the revised structure; this entry moves to `Status: Superseded by D-NNN`. The standard's own backward-compatibility rule means existing projects continue to work under the prior structure even after a successor decision is recorded.
