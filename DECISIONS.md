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
- **Fixed status vocabularies** (project status: Active / Dormant / Complete / Archived / Superseded; decision status: Proposed | Accepted | Superseded | Deprecated; claim status: Proposed | Supported | Refuted | Withdrawn) so tooling can parse without ambiguity.
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

---

### D-002 Add `skeletons/` directory rather than a separate usage guide

**Date:** 2026-05-13
**Status:** Accepted
**Authors:** Shane Hartley; Claude (review session)
**Related:** D-001; `skeletons/` directory contents

**Context.** Once the standard was published, the next obvious gap was practical adoption support. The standard tells you the rules but doesn't address the blank-page problem when sitting down to write a first `FEATURES.md`, `DECISIONS.md`, or `ATTACK_VECTORS.md`. Three options for closing the gap were considered.

**Options.**

- **A. `USAGE.md` / `HOWTO.md` — prose how-to covering common scenarios.** "Starting a new software project," "Adapting an existing project," "Reviving a Dormant project," etc. Rejected: most of the content would duplicate the Creation Order, Workflow Variations, and Quick Decision Guide sections already in the standard. The remainder would be edge cases that may never arise. The standard's own cost note discourages writing documentation against confusion that hasn't occurred — the friction test fails.

- **B. `examples/` directory with annotated worked examples (e.g. a sample `FEATURES.md` for a software project, a sample `CLAIMS.md` for a research project).** Considered. Defers, not rejects: worked examples are genuinely useful but need to be realistic enough to teach without being so domain-specific that they only apply to one type of project. Drafting good examples is a heavier task than skeleton-extraction and is better done once external users (or own use) reveal which examples would help most.

- **C. `skeletons/` directory with copy-paste-ready starter files for each document type.** Chosen. Each skeleton is the structure already specified in the standard, lifted out as a standalone file with placeholders marked and a brief header comment pointing back to the relevant standard section.

**Decision.** Option C. Add a `skeletons/` directory containing one `*.skeleton.md` file per document type the standard defines a skeleton for in the **Minimal File Skeletons** section: README, FEATURES, CLAIMS, DECISIONS, ATTACK_VECTORS, ROADMAP, CLAUDE, CHANGELOG. Include a directory `README.md` explaining the copy-rename-fill workflow and a table mapping each skeleton to its tier.

Skeletons for ARCHITECTURE, SPEC, BUILD, and other Tier 3 docs (VOCABULARY, TESTING, SECURITY, CONTRIBUTING, BENCHMARKS) are deliberately not included — their content is too project-specific to template usefully. The standard's per-document specifications give enough structure to start from a blank file for those.

**Consequences.**

- New projects can scaffold their Tier 1 documents in seconds rather than copy-pasting from the standard's code blocks.
- Skeletons are short and schema-only, so maintenance burden is minimal. When the standard's skeletons change, the corresponding skeleton files must be updated to match — but the inline reference comment in each (`See: development_documentation.md §...`) makes the dependency explicit.
- The decision deliberately leaves room for worked examples (Option B) as a later addition, triggered by external interest in the repo or by friction the skeletons alone don't address.
- The decision deliberately rejects the larger usage-guide approach (Option A) on the basis of the friction test. If usage confusion arises later that the skeletons don't resolve, this rejection is revisitable.

**Reversal conditions.** Revisit if any of the following hold:

- Users (including future-self) report that the skeletons are insufficient — they can fill in the placeholders but still don't know *when* to use which document or *how* to handle situations the standard's Creation Order doesn't cover. This would trigger Option B (worked examples) or Option A (prose how-to).
- The skeletons drift out of sync with the standard often enough that maintenance burden exceeds their adoption benefit. This would trigger consolidation back into the standard itself with no separate `skeletons/` directory.
- A pattern of recurring questions about a specific scenario emerges (e.g. how to fork a project, how to convert a non-conforming repo) that warrants its own document. That would be a new addition, not a reversal — Option A and Option C are not mutually exclusive.

---

### D-003 Add `PROMPTS.md` with three narrow bootstrapping prompts

**Date:** 2026-05-13
**Status:** Accepted
**Authors:** Shane Hartley; Claude (review session)
**Related:** D-002; `PROMPTS.md`

**Context.** The standard's opening guidance ("drop this file into a chat session") tells users what to *do* with the file but not what to *say* in the opening message. For the three most common starting scenarios — new project, existing repo audit, Dormant revival — the right opening framing is non-obvious enough that users would otherwise face a back-and-forth opening before any real work begins. D-002 explicitly left room for this kind of addition by rejecting the broad usage guide (Option A) while not foreclosing narrower aids.

**Options.**

- **A. No prompts file; rely on the standard's intro line.** Rejected: the intro line is sufficient for telling Claude what conventions to follow, but insufficient for framing the session task. Users would still need to phrase the opening themselves and would likely under-specify on first attempt.

- **B. Exhaustive prompts file covering many scenarios** (e.g. fork a project, convert a non-conforming repo, port between standards, generate a CHANGELOG from git history, etc.). Rejected: this is Option A from D-002 re-emerging under a different name. The same friction-test argument applies: most scenarios are edge cases that may never arise, and a long prompts file is prone to staleness and bloat.

- **C. Narrow prompts file with three carefully chosen scenarios.** Chosen. Three covers the high-frequency cases (new / audit / revive) without sliding into the broad-guide failure mode.

**Decision.** Option C. Add `PROMPTS.md` at the repo root containing exactly three starter prompts:

1. **Bootstrap a new project** — walks Claude through Creation Order with explicit instruction to ask questions before drafting.
2. **Audit an existing repo** — leverages the friction test from the cost note; orders proposed additions by leverage.
3. **Revive a Dormant project** — produces a status report before resuming work; references the Project Lifecycle section and reversal conditions.

The file frames itself as a bootstrapping aid for sessions where no `CLAUDE.md` exists yet, and closes with the explicit note that once a `CLAUDE.md` is created the normal flow applies (Claude reads `CLAUDE.md` first). This matters: the prompts file is not a guide to ongoing use, only to the cold-start problem.

**Consequences.**

- The cold-start friction for new projects, audits, and revivals is reduced from "compose an opening message from scratch" to "copy a prompt, fill in the project name."
- The file's tight scope (three prompts, one paragraph each, plus framing notes) keeps maintenance burden minimal and makes drift easy to detect.
- The prompts deliberately keep Claude in planning / questioning mode rather than letting it dive into output, matching the standard's preference for scope-definition before implementation.
- The first real test of all this scaffolding is the self-application experiment: pointing Claude Code at this repo with the audit prompt and asking it to assess project-scaffold against its own standard. That will be the first concrete friction signal.

**Reversal conditions.** Revisit if any of the following hold:

- The three prompts prove insufficient for a recurring scenario (e.g. forking a project is asked about repeatedly). The response is a new prompt added to the file, not removal of the existing ones; if the file grows past ~6 prompts, the rejection of Option B becomes due for re-examination.
- A prompt produces consistently poor results on first attempt — e.g. Claude defaults to writing output rather than asking questions despite the prompt's instruction. The response is to tighten the prompt's framing, not to remove the file.
- The standard itself evolves such that the prompts reference sections that have moved or been renamed. Update the prompts to match; this is a routine sync, not a structural reversal.
- The self-application test reveals that the prompts are unnecessary because the standard's existing intro guidance is enough. This would be a real reversal and would warrant deleting the file rather than maintaining it.
