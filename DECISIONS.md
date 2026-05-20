# Decisions

Append-only log of significant design decisions for the project-scaffold repo.

Each entry: `D-NNN`, dated ISO 8601, with status, context, options, decision, consequences, and reversal conditions.

Status vocabulary: Proposed | Accepted | Superseded by D-NNN | Deprecated.

---

### D-001 Standard format: tiered documents, stable IDs, lifecycle vocabulary

**Decided:** 2026-05-13
**Recorded:** 2026-05-13
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

**Decided:** 2026-05-13
**Recorded:** 2026-05-13
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

**Decided:** 2026-05-13
**Recorded:** 2026-05-13
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

---

### D-004 Standard revisions following first self-audit

**Decided:** 2026-05-13
**Recorded:** 2026-05-13
**Status:** Accepted
**Authors:** Shane Hartley; Claude (review session, acting on self-audit findings from Claude Code session)
**Related:** D-001, D-002, D-003; the standard's revised Provenance log; `SELF_AUDIT.md` (untracked, diagnostic only)

**Context.** The first self-audit run against this repo (2026-05-13, using `PROMPTS.md` prompt 2 modified for recursive self-application) identified ten standard-level findings and seven repo-level conflicts. The highest-leverage finding was a logical contradiction inside the standard itself: the Tier 1 framing ("every project, no exceptions") directly conflicted with the cost note's friction test ("Skip a Tier 2 or Tier 3 doc when...", which implicitly denied Tier 1 the same treatment). The contradiction was not a meta-level quirk of this repo — it affects every project that legitimately omits a Tier 1 document for principled reasons (documentation-only repos, solo toy projects, throwaway experiments). Two drafting sessions had not caught it.

**Options considered.**

- **A. Treat the audit findings as repo-only and leave the standard unchanged.** Rejected: the Tier 1 contradiction is in the standard, not in the repo's application of it. Leaving it would propagate the contradiction to every future user.

- **B. Address every finding from the audit in one large revision.** Rejected: some findings are minor or judgement-call (e.g. refreshing Last reviewed without a textual edit) and bundling them with load-bearing changes would obscure rationale. Better to act on the high-leverage findings and defer the rest.

- **C. Action a coherent five-edit package — two standard changes (Tier 1 reconciliation, Documentation-as-deliverable Workflow Variation), three repo changes (CLAUDE.md, CHANGELOG sync, README map update), plus minor housekeeping for the standard itself (ATTACK_VECTORS detection rule, Evolution-section recursive-application paragraph, project-specific-extensions clause).** Chosen.

**Decision.** Option C. The five-edit package:

1. **Tier 1 framing reconciled with the cost note.** Header softened to "Default minimum (every project, with narrow documented exemptions)." Body text requires Tier 1 omissions to be recorded as `DECISIONS.md` entries. The cost note extended to explicitly cover Tier 1 with the same friction test plus the documented-exemption requirement.

2. **Documentation-as-deliverable Workflow Variation added** to the Creation Order section, parallel to AI-first and Research-driven. Spells out how Tier 1 documents adapt for non-code deliverables: which sections become N/A, which become "How to use" rather than "Quick Start," which are legitimate exemptions for documentation projects.

3. **ATTACK_VECTORS Maintenance Rule 4 softened** from "Detection is not optional" to "Detection is defined, not necessarily automated." Manual / structural review now explicitly named as a valid detection method, matching the spec's existing examples and preventing the rule from being unusable for documentation-style projects.

4. **Recursive-application paragraph added to Evolution section.** Explicit statement that the host repo follows the standard with documented exemptions, and that periodic self-audits are the recommended mechanism for catching drift and meta-level gaps. References the 2026-05-13 audit as the canonical case for what the recursive check is for.

5. **Project-specific-extensions clause added to Evolution section.** Lists reserved document names and the conditions under which projects may add document types beyond those the standard names (DECISIONS entry recording the reason, no name collisions, consistent conventions). Resolves the audit's §5.7 finding without enumerating every possible document type in the standard.

Plus the corresponding repo changes (CLAUDE.md added; CHANGELOG synced to record D-002, D-003, skeletons, PROMPTS.md; README documentation map updated). The repo changes are tracked in CHANGELOG `[Unreleased]` rather than retroactively modifying v0.1.0.

**Consequences.**

- The standard is now internally consistent. The Tier 1 / cost-note contradiction is resolved.
- The host repo's Tier 1 omissions (`FEATURES.md`, `ROADMAP.md`) become principled exemptions rather than violations, provided they are recorded in DECISIONS — see D-005 and D-006 below.
- Documentation-only projects (style guides, RFCs, standards, books, dataset documentation) have an explicit Workflow Variation to follow, rather than having to improvise.
- The standard now formally permits project-specific extensions. `PROMPTS.md` (an extension this repo added) is retrospectively legitimised via D-003; future projects can add similar extensions without violating the standard.
- Backward compatibility holds: no document types removed, no IDs renumbered. The five existing reserved names (`F-`, `C-`, `D-`, `AV-`, status vocabularies) are unchanged.
- The audit pattern itself is now part of the standard's recommended practice, not just an ad-hoc experiment. Future self-audits or audits of other projects use the same prompt and produce comparable artifacts.

**Reversal conditions.** Revisit if any of the following hold:

- The softened Tier 1 framing produces drift in practice — i.e. projects start exempting Tier 1 documents without writing DECISIONS entries, and the exemptions accumulate as silent omissions. Response: tighten enforcement guidance, possibly add a `tools/check_tier1_exemptions.py` to the standard's recommended tooling.
- The Documentation-as-deliverable variation proves under-specified — a real documentation project tries to apply it and reports that critical adaptation cases are missing. Response: extend the variation rather than reverse it.
- A subsequent self-audit on this repo or another finds new contradictions in the standard introduced by these changes. Response: revise; this is the standard doing its job.
- Project-specific extensions multiply to the point where the reserved-names list is restrictive or the no-collision rule produces conflicts. Response: revisit the extension clause, possibly with a namespace convention.

---

### D-005 Tier 1 exemption: `FEATURES.md`

**Decided:** 2026-05-13
**Recorded:** 2026-05-13
**Status:** Accepted
**Authors:** Shane Hartley; Claude (review session)
**Related:** D-001, D-004; the standard's Documentation-as-deliverable Workflow Variation

**Context.** Following the Tier 1 framing softening (D-004), Tier 1 omissions are permitted but must be recorded as DECISIONS entries naming the document, the reason, and the revisit conditions. This repo's primary deliverable is `development_documentation.md` — a standard document — not a software tool with capabilities. The conventional content of `FEATURES.md` (MoSCoW-prioritised capabilities with acceptance criteria) does not map naturally onto a documentation deliverable.

**Decision.** Exempt this repo from `FEATURES.md`. The repo's "features," in the conventional sense, are the standard's tier system, stable ID conventions, status vocabularies, and lifecycle transitions — all of which are documented in the standard itself (§Document Tiers, §Per-Document Specifications, §Project lifecycle). Duplicating this content into a separate `FEATURES.md` would create a maintenance burden with no signal value.

**Consequences.**

- The repo has no `FEATURES.md`. The CHANGELOG and DECISIONS entries reference document types in `development_documentation.md` directly rather than via `F-NNN` IDs.
- `D-002` and `D-003` (which reference companion artifacts) point at filenames (`skeletons/`, `PROMPTS.md`) rather than stable feature IDs. This is acceptable for now; if companion artifacts multiply, the exemption stops being free.

**Reversal conditions.** Reverse this exemption (i.e. add a real `FEATURES.md` to the repo) if any of the following hold:

- The repo accumulates companion artifacts (`examples/`, validation scripts, sibling documents) such that referring to them by filename in DECISIONS / CHANGELOG becomes ambiguous or brittle.
- The standard begins versioning components independently (e.g. the tier system gets revised independently of the lifecycle vocabulary), and stable IDs would help track which component is at which version.
- Adoption grows to the point where users frequently ask "what does this repo deliver?" — at which point a clear capability list earns its place.

---

### D-006 Tier 1 exemption: `ROADMAP.md`

**Decided:** 2026-05-13
**Recorded:** 2026-05-13
**Status:** Accepted
**Authors:** Shane Hartley; Claude (review session)
**Related:** D-001, D-004; the standard's Evolution section

**Context.** The standard isn't built in phases; it is revised inline as material findings emerge (the inline Provenance log in the standard's header is the audit trail). A `ROADMAP.md` listing "Phase 1: foundation, Phase 2: ..., Phase 3: ..." would be either fiction or a duplicate of the Provenance log.

**Decision.** Exempt this repo from `ROADMAP.md`. The standard's own Provenance log, plus this DECISIONS.md, plus the CHANGELOG, together capture the project's history and forward intent without need for a separate phased plan.

**Consequences.**

- The repo has no `ROADMAP.md`. Planning is captured implicitly: short-term in CHANGELOG `[Unreleased]`, medium-term in DECISIONS reversal conditions (which name the triggers that would prompt future work), long-term in the standard's Provenance log of completed material revisions.
- No "Active → Complete" transition checklist item references `ROADMAP.md` for this repo. The standard's lifecycle section has been updated (D-004) to permit exempted-document checklist items to be skipped.

**Reversal conditions.** Reverse this exemption (i.e. add a real `ROADMAP.md` to the repo) if any of the following hold:

- The standard reaches sufficient complexity that material revisions need to be planned in phases (e.g. "v1.0 deprecates X; v1.1 adds Y; v2.0 reorganises the tier system") rather than landing as ad-hoc inline revisions.
- The repo grows enough infrastructure (tooling, examples, sibling documents) that coordinating their evolution becomes a planning task in its own right.
- The standard reaches sufficient adoption that external users need visibility into upcoming changes (i.e. a public roadmap becomes a feature).

---

### D-007 Standard revisions following second self-audit (Arithmancy)

**Decided:** 2026-05-13
**Recorded:** 2026-05-13
**Status:** Accepted
**Authors:** Shane Hartley; Claude (review session, acting on self-audit findings from Claude Code session against the Arithmancy repo)
**Related:** D-001, D-004; Arithmancy `SELF_AUDIT.md` (untracked, diagnostic only)

**Context.** The second self-audit run was a recursive application of `PROMPTS.md` prompt 2 (modified for the Complete-state case) against the Arithmancy repo — a CUDA/C++ Mersenne-prime engine asserted as Complete but not yet declared so. The audit surfaced five standard-level findings, all independently actionable, in addition to thirteen repo-level recommendations specific to Arithmancy.

The Arithmancy-specific recommendations are Shane's responsibility to action in his own repo. This entry covers only the standard-level changes that land in `project-scaffold` itself.

**Standard-level findings (from audit §5):**

1. **Retroactive completion path is unspecified.** The Active → Complete checklist references documents the standard would have built up during Active phase. For late-adopting projects, every item is vacuously unmet; the transition cannot be honestly ticked.
2. **Friction test is post-hoc; Complete projects need a forward-looking variant.** The present-tense friction test ("are you currently confused?") fires for nothing when no one is currently developing. But Complete is precisely when future-revival cost matters most.
3. **`CLAUDE.md` spec implicitly assumes Active state.** For Complete projects the document's role shifts from handoff-for-continuation to handoff-for-revival; the section shape needs to adapt.
4. **Retroactive DECISIONS entries have ambiguous date semantics.** A single `Date:` field cannot capture both when a decision was made and when it was documented; these diverge significantly for retroactive entries.
5. **ATTACK_VECTORS `Detection: not implemented` is itself signal.** For Complete projects whose verification machinery was never operationalised (Arithmancy's Gerbicz check, asynchronous checkpointing), the honest entry reads "Detection: not implemented." The standard's previous wording ambiguously suggested this was unacceptable.

**Options considered.**

- **A. Defer the standard changes; address only Arithmancy.** Rejected. All five findings are general to projects following the standard, not specific to Arithmancy. The Complete-state lifecycle is genuinely underspecified; leaving the gaps in place propagates them to every future Complete-state project.
- **B. Bundle the changes into a single revision pass.** Chosen. The five findings are mutually reinforcing — the Retroactive Completion path explicitly references the Forward-Revival friction test; the Complete-state `CLAUDE.md` variant references both; the date-field convention is needed for retroactive DECISIONS entries that the Retroactive Completion path explicitly requires. Bundling them produces a coherent Complete-state story rather than five disconnected edits.

**Decision.** Option B. Five revisions to the standard:

1. **New §Project lifecycle subsection: Retroactive completion.** Specifies the minimum acceptable path for a project that finishes development without having adopted the standard during Active phase — status header update + single sealing DECISIONS entry covering bulk exemptions and divergences + optional CLAIMS audit pass for projects with empirical claims in marketing prose. Explicitly notes that retroactive completion is not a discount on the standard but a recognised path that produces a smaller honest set of documents.

2. **New paragraph in §A note on cost: Future-revival friction test.** Forward-tense variant of the friction test, triggered by Complete-state transitions. Threshold tiers (mandatory / strongly recommended / case-by-case) framed around the "would absence force archaeology rather than execution?" question.

3. **New §Workflow variations entry: Complete-state projects.** Sits alongside AI-first, Research-driven, and Documentation-as-deliverable. Spells out the four-section adaptation: Current state → Frozen state at completion; Active task → Revival triggers; Out of scope (with added weight); new section "What to read first on revival." Notes that the Complete-state CLAUDE.md is typically half the length of an Active-state one because it orients toward a decision to begin work, not toward work itself.

4. **DECISIONS entry skeleton revised: Decided / Recorded date fields.** The single `Date:` field is replaced with two: `Decided:` (when the choice was made) and `Recorded:` (when the entry was written). For normal entries both are identical; for retroactive entries they diverge. Either field alone is acceptable when the other is unknown. The convention is added to the standard's entry-format example, file-header description, and skeleton file under `skeletons/DECISIONS.skeleton.md`. The six existing entries in this repo's `DECISIONS.md` were migrated to the new format (all six are non-retroactive, so both dates are 2026-05-13).

5. **ATTACK_VECTORS Maintenance Rule 4 extended.** Detection is now defined as falling into three categories: implemented automated, implemented manual, and acknowledged-but-not-implemented. The third option (`Detection: not implemented (would require X); see CLAIMS C-NNN`) is now first-class — particularly relevant for Complete-state projects whose claimed verification was never operationalised, and for early-Active projects where vectors are identified before detection tooling exists. An undetected vector is itself signal; the rule's intent (no undefined detection) is preserved by requiring one of the three categories.

**Consequences.**

- Complete-state lifecycle transitions are now well-defined for both standard-adopting-from-day-one projects and standard-adopting-at-completion projects. The Arithmancy-style situation has a recognised path.
- The forward-revival friction test makes Complete-state documentation decisions principled rather than vacuous. Projects can apply the same operational test to both Active and Complete phases without contradiction.
- AI-assisted revival of Complete projects has explicit guidance via the Complete-state `CLAUDE.md` variant. Future sessions opened against a Complete project's repo will read the right shape of context document.
- Retroactive DECISIONS entries are now syntactically distinguishable from normal ones, preserving audit traceability across both fresh and backfilled cases.
- ATTACK_VECTORS entries can now be honest about unimplemented verification without violating the detection rule. The Arithmancy audit's finding (Gerbicz check claimed in README, not implemented in V2.0.0-GOLD) becomes recordable as a legitimate vector with `Detection: not implemented`.
- Backward compatibility holds. Existing DECISIONS entries using single `Date:` are not invalid — the migration to Decided/Recorded is a recommended update, not a requirement. No document types removed; no IDs renumbered.

**Reversal conditions.** Revisit if any of the following hold:

- The Retroactive Completion path produces drift in practice — projects use it to skip documentation work that the forward-tense friction test would have required. Response: tighten the "Mandatory" threshold in the forward-revival test, possibly require a CLAIMS audit pass rather than marking it optional.
- The Decided/Recorded date convention causes confusion in practice (people unsure which to fill, or both repeatedly identical making the second field feel ceremonial). Response: simplify back to a single `Date:` field with annotations for retroactive cases, accepting the audit-traceability loss.
- A third self-audit (or external user report) finds that the Complete-state `CLAUDE.md` variant is still under-specified for some workflow we haven't anticipated. Response: extend the variant rather than reverse it.
- The "not implemented" detection option leads to projects shipping with many such entries and never operationalising the detection. Response: add a maintenance rule that "Detection: not implemented" entries trigger periodic review and either implementation or downgrade to "Withdrawn." This would be an additive rule, not a reversal.

---

### D-008 Add `BUGS.md` as a Tier 2 document type

**Decided:** 2026-05-21
**Recorded:** 2026-05-21
**Status:** Accepted
**Authors:** Shane Hartley; Claude (review session)
**Related:** D-010 (the workflow rule that makes BUGS.md load-bearing); the standard's §Per-Document Specifications and `skeletons/BUGS.skeleton.md`

**Context.** Working on `tux-ti83` (a TI-83 calculator emulator) over several months, Shane developed a `BUGS.md` file with stable IDs (`BUG-NNN`), a fixed status vocabulary (open / fixed / wontfix / deferred), and a strict workflow rule: bugs are logged when found, not silently fixed; the user decides whether to fix immediately, defer, or leave alone. The format proved useful enough — across multiple sessions, multiple AI-assisted reviews, and one user-visible regression caught only because a prior bug entry made the failure mode legible — that it should be promoted from a one-project pattern to a standard-prescribed document type. The standard already has `ATTACK_VECTORS.md` for *anticipated* failure modes with detection methods (forward-looking) but no slot for *realised* failures with status (backward-looking). The two are complementary, not redundant.

**Options.**

- **A. Treat bugs as a subset of `ATTACK_VECTORS.md` entries.** Rejected: ATTACK_VECTORS demands a detection method per entry and is structured as a checklist of properties the system must hold. Bugs are historical incidents — they have status, reproduction steps, and a fix path. Conflating the two would dilute both and make ATTACK_VECTORS less useful as a forward-looking gate.

- **B. Delegate to GitHub Issues / Jira / Linear without prescribing a `BUGS.md`.** Rejected: external trackers are the right call for many teams, but (a) solo-dev and AI-partner workflows benefit from a single in-repo file an AI agent can read without API access, (b) in-repo bug history survives forge migrations and external-service deprecation, (c) the discipline-rule ("log when found, not silently fixed" — see D-010) is harder to enforce when the bug catalogue lives outside the repo. The standard should support both — `BUGS.md` for in-repo workflows, external trackers when projects prefer them. Tier 2 placement (strongly recommended, not mandatory) reflects this.

- **C. Add `BUGS.md` to Tier 2 with `BUG-NNN` stable IDs, status vocabulary (open / fixed / wontfix / deferred), the entry format from `tux-ti83`, and the workflow rule (recorded separately as D-010).** Chosen.

**Decision.** Option C. The standard prescribes `BUGS.md` as a Tier 2 document for projects that want their bug catalogue in-repo. The format mirrors `tux-ti83`'s `BUGS.md`:

- **Stable IDs.** `BUG-001`, `BUG-002`, …, append-only. Referenced from commits, CHANGELOG entries, ATTACK_VECTORS (when a recurring bug pattern warrants a new vector), and DECISIONS (when a bug fix is significant enough to be a decision).
- **Status vocabulary.** open | fixed | wontfix | deferred. Fixed values; tooling and AI partners parse them mechanically.
- **Entry fields.** Status; Found (YYYY-MM-DD with session/commit context); Location (path:line); Severity (low | medium | high); Description; Reproduction (when known); Notes (related context, suggested fix, links).
- **File organisation.** Sections by status (Open / Fixed / Won't Fix / Deferred). Each entry sits under the section matching its current status; the entry's `Status:` field is the source of truth.
- **Relationship to ATTACK_VECTORS.** ATTACK_VECTORS lists what *could* go wrong with detection methods (forward-looking checklist); BUGS lists what *did* go wrong with status flags (backward-looking incident log). A recurring bug pattern may warrant a new ATTACK_VECTORS entry; an ATTACK_VECTORS hit that escaped detection in production becomes a BUG entry. Cross-references are bidirectional.

The "log when found, not silently fixed" discipline that makes BUGS.md valuable is recorded as a separate Maintenance Rule (see D-010) rather than baked into this document's per-doc spec, because the rule applies equally to IMPROVEMENTS.md (D-009) and is behavioral guidance for AI partners and humans rather than document content.

**Consequences.**

- Projects gain a standard-prescribed in-repo bug catalogue. `BUG-NNN` becomes the fifth stable-ID namespace alongside `F-`, `C-`, `D-`, `AV-`.
- `BUGS.md` joins `BUGS` on the reserved-names list in the Evolution section's project-specific-extensions clause.
- CHANGELOG's `### Fixed` section now references `BUG-NNN` IDs naturally alongside the existing `AV-NNN` pattern, giving traceability for what was fixed and when.
- The Quick Decision Guide gains a new entry pointing at BUGS.md ("Are you tracking discovered bugs in-repo rather than in an external tracker?").
- Tier 2 (not Tier 1) placement means projects using GitHub Issues or another tracker are not violating the standard by omitting BUGS.md. The friction test applies: if the in-repo catalogue would be a burden duplicating an external one, skip it.
- A new skeleton (`skeletons/BUGS.skeleton.md`) is added so adopters can copy-paste-fill.
- This repo does not currently have a `BUGS.md`. Per the Tier 2 friction-test override, no DECISIONS entry is required for the omission; the absence is recorded by inference (no friction signal has fired) and revisited if drift becomes visible.

**Reversal conditions.** Revisit if any of the following hold:

- Users report that maintaining `BUGS.md` alongside GitHub Issues / Jira / equivalent is redundant friction with no compensating benefit. Response: move BUGS.md to Tier 3 with an explicit "only when no external tracker is in use" trigger, rather than Tier 2's broad "strongly recommended."
- The BUG-/AV- distinction proves consistently confusing in practice — users repeatedly file entries in the wrong document or duplicate them across both. Response: clarify the boundary in both per-document specs with worked examples, or, if the conflation is genuine, merge them into a single document with two entry types.
- The four-value status vocabulary proves insufficient (e.g. a "needs-info" or "blocked-on-external" state recurs across projects). Response: extend the vocabulary in a new revision; existing entries are not invalidated because the values are additive.

---

### D-009 Add `IMPROVEMENTS.md` as a Tier 2 document type

**Decided:** 2026-05-21
**Recorded:** 2026-05-21
**Status:** Accepted
**Authors:** Shane Hartley; Claude (review session)
**Related:** D-008 (parallel document for realised bugs); D-010 (the workflow rule that makes both BUGS and IMPROVEMENTS load-bearing); the standard's §Per-Document Specifications and `skeletons/IMPROVEMENTS.skeleton.md`

**Context.** The same `tux-ti83` development that produced `BUGS.md` (see D-008) also produced an `IMPROVEMENTS.md` — the dual catalogue, recording proposed refactors, architectural changes, and code-quality wins (stable IDs `IMP-NNN`, status vocabulary suggested / applied / declined / deferred, the same "log when noticed, not silently applied" discipline). The format proved useful because it occupies a niche neither `FEATURES.md` nor `DECISIONS.md` covers cleanly: a candidate `IMP-NNN` is not yet a committed capability (so it doesn't belong in FEATURES), and it is not yet a decided choice between alternatives (so it doesn't belong in DECISIONS). It's a tracked suggestion — visible to the maintainer, available for the user to act on or decline, surviving session boundaries.

Several `BUG-NNN` entries in `tux-ti83`'s BUGS.md reference `IMP-NNN` improvements ("structural cleanup logged as IMP-001"), confirming the documents are paired in practice.

**Options.**

- **A. Treat improvements as candidate features in `FEATURES.md`'s "Candidate features (uncommitted)" section.** Rejected: candidate features are uncommitted *user-facing capabilities*; improvements are uncommitted *internal changes* (refactors, performance tweaks, dead-code removal, architectural cleanups). Conflating them either dilutes FEATURES (mixing user-visible and internal scope) or strands real internal-quality items because they don't read as "features." The orthogonal-axes argument that motivates `FEATURES.md` / `CLAIMS.md` separation applies here too: features are user-facing commitments, improvements are maintainer-facing candidates.

- **B. Treat improvements as proposed-status `DECISIONS.md` entries.** Rejected: DECISIONS entries record a *choice between alternatives* with reversal conditions. An improvement candidate is at an earlier stage — the question isn't "which alternative?" but "is this worth doing at all?" Forcing every improvement candidate through DECISIONS would either inflate the decision log with non-decisions or pressure authors to skip the candidate stage entirely.

- **C. Add `IMPROVEMENTS.md` to Tier 2 with `IMP-NNN` stable IDs, status vocabulary (suggested / applied / declined / deferred), the entry format from `tux-ti83`, and the same workflow rule as BUGS (D-010).** Chosen.

**Decision.** Option C. The standard prescribes `IMPROVEMENTS.md` as a Tier 2 document for projects that want a tracked, persistent list of candidate refactors and improvements. The format mirrors `tux-ti83`'s `IMPROVEMENTS.md`:

- **Stable IDs.** `IMP-001`, `IMP-002`, …, append-only. Referenced from commits, CHANGELOG (when applied), BUGS (when a bug fix surfaces an improvement candidate or vice versa), and DECISIONS (when a decision is needed before applying).
- **Status vocabulary.** suggested | applied | declined | deferred.
- **Entry fields.** Status; Found (YYYY-MM-DD with session/commit context); Location (path:line or "cross-cutting"); Effort (trivial | small | medium | large); Description (what could be improved and why); Proposal (how to do it); Trade-offs (what we'd give up or risk); Notes (related context, dependencies on other work).
- **File organisation.** Sections by status (Suggested / Applied / Declined / Deferred), same pattern as BUGS.
- **Trade-offs are not optional.** An entry without `Trade-offs:` is a feature request, not an improvement candidate. The trade-off field is what makes the entry useful for later adjudication — without it, the entry can't be evaluated when revisited.
- **Relationship to BUGS.** Bugs are things that are *broken*; improvements are things that *work but could be better*. The distinction is sharp enough to file an entry in exactly one document. When a bug fix surfaces an improvement candidate, the BUG entry references the IMP and vice versa.
- **Relationship to FEATURES.md.** Features are user-facing committed capabilities (with acceptance criteria); improvements are internal-facing candidate changes (with trade-offs). Applied improvements may motivate updates to FEATURES if user-visible behavior shifts; pure-internal improvements don't.

The same workflow rule (D-010) governs IMPROVEMENTS as BUGS: log when noticed, not silently apply; the author decides whether to act, defer, or decline.

**Consequences.**

- Projects gain a standard-prescribed in-repo improvement catalogue. `IMP-NNN` becomes the sixth stable-ID namespace alongside `F-`, `C-`, `D-`, `AV-`, `BUG-`.
- `IMPROVEMENTS.md` joins the reserved-names list.
- CHANGELOG's `### Changed` section references `IMP-NNN` IDs naturally when improvements land.
- Tier 2 placement matches BUGS — strongly recommended for projects that benefit from in-repo tracking; legitimately exempt for projects using external trackers or for projects too small to need the discipline.
- A new skeleton (`skeletons/IMPROVEMENTS.skeleton.md`) is added.
- This repo does not currently have an `IMPROVEMENTS.md`. Same friction-test reasoning as D-008 for the absence: no IMP candidates currently in flight; revisit if drift becomes visible.

**Reversal conditions.** Revisit if any of the following hold:

- Improvements consistently get filed in `DECISIONS.md` or `FEATURES.md` instead, with users reporting that IMPROVEMENTS.md duplicates one of those. Response: clarify the per-document distinctions with worked examples, or, if the conflation is genuine, retire IMPROVEMENTS into one of the other documents.
- The four-value status vocabulary proves insufficient (e.g. an "in-progress" state recurs because applied improvements take multiple sessions). Response: extend additively.
- The Effort field becomes either ceremonial (everything filed as "medium") or contentious (estimates routinely wrong by an order of magnitude). Response: drop the field, or replace it with a coarser "small / large" binary. Existing entries are not invalidated.

---

### D-010 Maintenance Rule 8 — "Log when found, not silently acted on"

**Decided:** 2026-05-21
**Recorded:** 2026-05-21
**Status:** Accepted
**Authors:** Shane Hartley; Claude (review session)
**Related:** D-008 (BUGS.md); D-009 (IMPROVEMENTS.md); the standard's §Maintenance Rules

**Context.** Both `BUGS.md` (D-008) and `IMPROVEMENTS.md` (D-009) only earn their value if they're maintained with a specific discipline: bugs and improvement candidates discovered during work on something else are *logged*, not silently fixed or applied inline. Without this rule, the catalogues decay — entries get filed late, post-hoc, or not at all; in-flight scope creeps silently as an AI partner or human "helpfully" patches a discovery rather than logging it. The catalogue's value is its completeness; the rule is what produces completeness.

This is especially load-bearing for AI-partner workflows. AI partners default to acting on discoveries — given an instruction to refactor function A, an AI agent that notices a latent bug in function B will frequently just fix B too, with a sentence in the commit message. The fix may be correct, but it bundles two changes into one and bypasses the user's decision on whether to defer, decline, or fix immediately. For human contributors the same drift happens more slowly but with the same effect: a six-month-old codebase has dozens of opportunistic fixes the original session never tracked.

The rule applies whenever BUGS.md or IMPROVEMENTS.md exists in a project. Where neither exists, the rule is moot.

**Options.**

- **A. Embed the rule in BUGS.md and IMPROVEMENTS.md per-document specs only, without a top-level Maintenance Rule.** Rejected: the rule is behavioral guidance for AI partners and human contributors, not document content. The standard's existing Maintenance Rules ("Docs are part of the commit," "CLAUDE.md is current state, not history") are also behavioral; this rule belongs in the same family. Embedding it only in per-doc specs underweights it.

- **B. Add as Maintenance Rule 8 at the top level, with cross-references from BUGS.md and IMPROVEMENTS.md per-doc specs.** Chosen.

**Decision.** Option B. Add Maintenance Rule 8 to the standard's §Maintenance Rules section:

> **Log when found, not silently acted on.** When a bug is discovered or an improvement candidate is noticed during work on something else, log it in `BUGS.md` / `IMPROVEMENTS.md` rather than fix or apply it inline. The author (or, for AI-partner workflows, the user) decides whether to act immediately, defer, or decline. This rule is what makes BUGS and IMPROVEMENTS useful catalogues: their value is completeness, and completeness requires that in-flight discoveries are recorded before they evaporate into commit-message footnotes.
>
> Applies only when BUGS.md and/or IMPROVEMENTS.md exist in the project. Where neither exists, the rule is moot.

The BUGS.md and IMPROVEMENTS.md per-document specs reference this rule rather than restating it, keeping the source of truth in the Maintenance Rules section.

**Consequences.**

- AI partners reading `CLAUDE.md` and the standard now have an explicit behavioral commitment: do not silently fix bugs or apply improvements when working on something else. Log them; let the user decide.
- The rule formalises the existing `tux-ti83` workflow practice as a standard-level commitment, applicable to any project adopting BUGS or IMPROVEMENTS.
- Maintenance Rule 8 joins the existing seven; the numbering remains stable (rule 8 is additive, not a reordering).
- The rule introduces a small ritual cost — every in-flight discovery becomes a log entry rather than a silent fix. For trivial fixes (typo in a comment) this can feel like overhead; the spec language frames it as a default with judgement-call exceptions ("the user decides").

**Reversal conditions.** Revisit if any of the following hold:

- The log-cost becomes burdensome in practice — entries proliferate with no action ever taken, the user spends more time triaging the catalogue than the catalogue's existence saved them in scope-creep prevention. Response: relax the rule for trivial-severity entries, or downgrade it from a Maintenance Rule to a per-document recommendation in BUGS / IMPROVEMENTS specs.
- AI partners systematically misinterpret the rule and over-log (every minor decision becomes a BUG or IMP entry, polluting the catalogues with non-issues). Response: tighten the rule's language with explicit "what counts as a discovery" criteria, or add per-document severity thresholds below which logging is optional.
- A documented case emerges where the rule produced the wrong outcome — e.g. an AI partner logged a critical bug as `Status: open` mid-session when fixing it inline would have prevented a downstream failure in the same session. Response: add explicit guidance that critical-severity bugs may be fixed inline provided they are still logged after-the-fact, with the fix referenced.
