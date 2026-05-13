# Self-audit: project-scaffold against its own standard

**Date:** 2026-05-13
**Auditor:** Claude (recursive self-application of `development_documentation.md`)
**Subject:** the `project-scaffold` repo, treating `development_documentation.md` as the standard against which to assess the repo that houses it.

---

## 1. Repo state summary

The repo is the home of the **Development Documentation Standard** — a single normative document (`development_documentation.md`) defining the structural docs every project should carry, plus supporting material that helps users adopt it.

Contents:

- [`development_documentation.md`](development_documentation.md) — the standard. Tiered document set (1 mandatory / 2 strongly recommended / 3 conditional), stable ID conventions (`F-`, `C-`, `D-`, `AV-`), fixed status vocabularies, lifecycle transitions, tooling integration contract. ~38 KB.
- [`README.md`](README.md) — front door. Status header (`Active`, last reviewed 2026-05-13).
- [`DECISIONS.md`](DECISIONS.md) — three accepted decisions (D-001 standard format, D-002 skeletons directory, D-003 PROMPTS.md).
- [`CHANGELOG.md`](CHANGELOG.md) — Keep a Changelog format, version 0.1.0 dated 2026-05-13.
- [`LICENSE`](LICENSE) — CC BY 4.0.
- [`PROMPTS.md`](PROMPTS.md) — three cold-start prompts (new project / audit / dormant revival).
- [`skeletons/`](skeletons/) — eight copy-paste-ready starter files plus an index README.

**Status:** Active, first public release. Main artifact is the standard itself; everything else exists to make adoption easier. No code, no build, no tests.

---

## 2. Gaps identified

Documents the standard prescribes that this repo lacks, with the friction test applied to each.

### FEATURES.md (Tier 1)

- **Friction signal:** weak. Nobody (so far) has asked "what does this project offer?" — the README answers that adequately. But D-002 references "the `skeletons/` directory contents" and D-003 references PROMPTS.md without stable feature IDs; if this repo grew companion artifacts (e.g. an `examples/` directory, a cross-ref linter), the DECISIONS entries would have no stable IDs to point back at, and the CHANGELOG would lose its `F-NNN` references.
- **Recommendation:** **defer.** The friction test doesn't fire today. Revisit if companion artifacts multiply or if the standard itself begins versioning components separately. Note: borderline candidate for meta-level exemption (see §3).

### ROADMAP.md (Tier 1)

- **Friction signal:** weak. The evolution log is captured inline in the standard's Provenance header and in DECISIONS. There is no separate phased plan, and none is currently needed.
- **Recommendation:** **defer.** Possible meta-level exemption (see §3).

### CLAUDE.md (Tier 1)

- **Friction signal:** **real.** This very audit session would have started faster with a `CLAUDE.md` telling me: "main artifact is `development_documentation.md`; when modifying, refresh its inline Provenance log and Last reviewed; the repo is the worked example of its own standard." Right now PROMPTS.md serves users of the standard, not contributors to the standard.
- **Recommendation:** **add.** Highest-leverage Tier 1 gap. Also makes the repo a worked example of its own Tier 1 rule.

### ARCHITECTURE.md (Tier 2)

- **Friction signal:** none. Two flat directories (root + `skeletons/`), one normative document, no modules to describe.
- **Recommendation:** **don't add.** Genuine meta-level exemption — the "architecture" of the standard is the tier system, which is documented in the standard.

### SPEC.md (Tier 2)

- The standard explicitly permits domain-named specs (`PHYSICS.md`, `PROTOCOL.md`). `development_documentation.md` *is* the spec for this repo, just under a different name. Not a gap.
- **Recommendation:** none — consider the standard itself the spec, possibly noting this explicitly in the README.

### BUILD.md (Tier 2)

- N/A. No build.
- **Recommendation:** **don't add.**

### ATTACK_VECTORS.md (Tier 3)

- **Friction signal:** weak but plausible. The standard has identifiable failure modes — skeletons drifting out of sync with the standard, Provenance log going stale, status vocabulary drift, cross-reference rot without enforcement tooling. D-002 and D-003 partially anticipate these as reversal conditions. An `AV-NNN` register would consolidate them.
- **Recommendation:** **defer** until a drift incident actually happens, then capture both the incident and the vector at once. Standard-level note: the trigger condition is on the watchlist.

### CONTRIBUTING.md (Tier 3)

- **Friction signal:** none yet. CC BY 4.0 invites attribution-style use, but no PRs or issues to date.
- **Recommendation:** **defer** until a first external contributor surfaces.

### TESTING.md / VOCABULARY.md / SECURITY.md / CITATION.cff / BENCHMARKS.md (Tier 3)

- N/A for a documentation-only repo.

---

## 3. Gaps deliberately not present (meta-level exemptions)

These are documents the standard prescribes but that don't apply meaningfully because the repo's deliverable *is* the standard.

- **FEATURES.md** — "features" of the standard are the tier system, stable IDs, lifecycle vocabulary, status header. Spelling these out as `F-001`..`F-004` would mostly duplicate the standard's own §Document Tiers. **Flagged as borderline:** if the repo accumulates companion artifacts that need stable IDs to reference from DECISIONS / CHANGELOG, the exemption stops being free.
- **ROADMAP.md** — the standard isn't built in phases; it's revised inline. Material revisions live in the standard's Provenance header (per the "Evolution of this standard" section). A phased plan would be a fiction.
- **ARCHITECTURE.md** — no modules.
- **SPEC.md** — the standard is its own spec.
- **BUILD.md** — no build.
- **CLAIMS.md** — not a research project.

**Cases I'm unsure about:**

- **FEATURES.md** — listed above as borderline. The standard's "Tier 1 — every project, no exceptions" framing makes me reluctant to call this a clean exemption.
- **CLAUDE.md** — I initially considered this a meta-level exemption (the repo's only contributors are humans plus Claude sessions that already have PROMPTS.md and the standard to read) but concluded it's a real gap. Documented in §2.
- **ATTACK_VECTORS.md** — the standard *does* have failure modes worth enumerating, but they don't have automated detection. The standard's own definition ("Detection is not optional") suggests this isn't a clean fit — could be either a real gap or a standard-level mismatch (see §5).

---

## 4. Conflicts (existing docs diverge from the standard)

### 4.1 README missing required sections

The standard's §Per-Document Specifications → README.md lists seven required sections in order. The current README has only four (status header, description, "How to use", documentation map, license — five if "How to use" is generously read as a Quick Start substitute). Missing or substituted:

- **Quick start** — replaced with "How to use," which is prose rather than the standard's prescribed "Real commands, not prose."
- **Build requirements** — absent (legitimately N/A, but not marked as such).
- **Project structure** — absent.

This is partly a conflict and partly a standard-level finding (see §5 — the README spec assumes a code project).

### 4.2 README documentation map omits two existing docs

The README links to DECISIONS, CHANGELOG, and the standard. It does **not** link to [`PROMPTS.md`](PROMPTS.md) or [`skeletons/`](skeletons/). The standard says the documentation map should link to docs "as applicable" — both apply, both are missing. Direct conflict.

### 4.3 CHANGELOG out of sync with DECISIONS

[`CHANGELOG.md`](CHANGELOG.md) records `D-001` against version 0.1.0 (2026-05-13). The `[Unreleased]` section is empty. But [`DECISIONS.md`](DECISIONS.md) now contains `D-002` (skeletons) and `D-003` (PROMPTS.md), both dated 2026-05-13, and the repo contains both the `skeletons/` directory and `PROMPTS.md`. The standard's CHANGELOG specification requires referencing `F-`, `C-`, `D-`, `AV-` IDs for traceability. Direct conflict.

Most likely fix: either (a) move D-002 / D-003 / skeletons / PROMPTS.md into the 0.1.0 entry (treating them as part of the initial release, since they all landed on the same day), or (b) add an `[Unreleased]` block listing them.

### 4.4 D-001 references "the standard itself" without a stable ID

`D-001` lists `Related: development_documentation.md (the standard itself)`. There is no stable ID for "the standard." This isn't a hard conflict — cross-referencing a single file by name is fine — but it's a soft drift signal: if the standard ever splits into multiple files, the reference is ambiguous. Minor.

### 4.5 Cross-reference enforcement is acknowledged-aspirational

Standard Maintenance Rule 6 says cross-references should be bidirectional, enforced by tooling, otherwise "acknowledge in `CLAUDE.md` that cross-references may be stale." This repo has no `CLAUDE.md` and no tooling, so neither the enforcement nor the acknowledgment is in place. Indirect conflict — chained to §2's CLAUDE.md gap.

### 4.6 standard's Last reviewed date vs recent activity

`development_documentation.md` carries **Last reviewed: 2026-05-12**, but PROMPTS.md (added 2026-05-13) and D-003 (2026-05-13) both reference and lean on the standard. The standard wasn't materially modified, so the date is technically defensible — but Maintenance Rule 1 says to refresh Last reviewed when the project is re-opened after a gap, which arguably applied during today's PROMPTS.md / D-003 session. Borderline conflict.

### 4.7 PROMPTS.md isn't in the standard's tier list

`PROMPTS.md` is a real document in the repo but isn't a recognised document type in `development_documentation.md`. D-003 records the decision to add it, so this is a deliberate extension rather than drift — but the standard doesn't have a slot or naming convention for "cold-start prompt aids." Soft conflict, also a standard-level finding (see §5.7).

---

## 5. Standard-level findings (where the standard fails this self-application)

This is the part you said matters most. I tried to be honest.

### 5.1 "Tier 1 — Always (every project, no exceptions)" contradicts the cost note

The Document Tiers table heading says **"every project, no exceptions."** The §A note on cost section says **"Skip a Tier 2 or Tier 3 doc when..."** — pointedly excluding Tier 1 from the friction-test override. But this very repo legitimately omits three Tier 1 docs (FEATURES, ROADMAP, CLAUDE) and a strict reading of the standard would call those omissions standard violations rather than exemptions. The cost note implicitly trusts that the friction test is universal; the tier table denies it for Tier 1. The two clauses contradict.

**Suggested resolution:** soften "no exceptions" to something like "Tier 1 is the default minimum; legitimate exemptions are narrow and require a DECISIONS entry recording the reason." That would make the repo's own omissions standard-compliant via D-NNN entries naming each one.

### 5.2 README per-document spec assumes a code project

Required sections include "Quick start — shortest path from clone to **running output**," "Build requirements — **toolchain, OS targets, key dependencies**," and "Project structure — top-level directory tree." For a documentation-only repo or a writing project, these sections are either N/A or trivially small. The spec has no guidance for documentation-as-deliverable projects.

**Suggested resolution:** add a short note to the README spec section: "For non-code projects (documentation, writing, datasets), Quick Start may be replaced by a 'How to use' paragraph; Build requirements and Project structure may be omitted if trivial." Or add a Workflow Variation entry (see §5.4).

### 5.3 CLAUDE.md spec assumes a code project

Required sections include "Build & test commands — exact commands to verify changes," "Architectural invariants," "Conventions — naming, formatting, **comment style**, **commit message format**." For a docs-only repo these are mostly empty. The spec gives no guidance on writing a useful CLAUDE.md for non-code work, which is part of why this repo hasn't produced one.

**Suggested resolution:** add a note that for non-code projects, CLAUDE.md should still exist but emphasises invariants and conventions over build/test/architecture.

### 5.4 No "documentation-as-deliverable" Workflow Variation

The Creation Order section has two variations: AI-first and Research-driven. There is no variation for "the deliverable is documentation itself." A meta-level project like this repo, a style guide, an RFC, or a writing project doesn't fit cleanly into either existing variation. Adding a third variation would let the standard self-apply without contradiction.

### 5.5 ATTACK_VECTORS "Detection is not optional" rules out non-automated vectors

The Attack Vectors spec demands every vector state a detection method. For a documentation standard, the natural failure modes (drift, contradiction, staleness) often don't have automated detection — they're caught by review, not by tests. Either the standard should permit "manual review" as a detection method (already implicit in the spec text "test path, tool, **manual review**" but contradicted by the harder rule lower down), or it should call out a "manual / structural" severity stripe.

### 5.6 Maintenance Rule 6's xref tooling has no home

Rule 6 prescribes a cross-reference checker (`tools/check_xrefs.py` is named as illustrative). For an individual project, the tool lives in that project's `tools/`. But where does the *reference implementation* live? In this repo? In a sibling repo? The standard doesn't say. This is the same recursive problem that motivates the audit — the standard prescribes tooling without specifying whose responsibility it is to build or host it.

### 5.7 No slot for cold-start prompt aids

`PROMPTS.md` is a useful document type for any project that expects fresh AI sessions to be common. The standard doesn't acknowledge it. Two ways to resolve: (a) add a Tier 3 entry for `PROMPTS.md` (cold-start aid for AI-assisted projects without a stable `CLAUDE.md` yet), or (b) explicitly delegate it to project-specific extensions, since this repo's adoption-tooling role is unusual.

### 5.8 The Tier 1 rule "every project … LICENSE" doesn't say which one for documentation

The standard says "Pick one before first public commit." For a code project, MIT/Apache/etc. are the usual menu. For a documentation standard (this repo), CC BY 4.0 is the natural fit — but the standard doesn't acknowledge that the right license depends on the deliverable type. Minor.

### 5.9 Project lifecycle Active → Complete checklist assumes FEATURES exists

The Active → Complete transition requires "all FEATURES.md Must-priority entries marked Complete or explicitly Withdrawn." If FEATURES.md was legitimately exempted (per §5.1), this checklist item is undefined. The lifecycle section should either state that exempted documents skip their checklist items, or rewrite the transitions to be document-agnostic.

### 5.10 Recursive question is partially answered

The "Evolution of this standard" section addresses self-application *of the document* (inline Provenance log, future promotion to its own DECISIONS.md). It does **not** address self-application *of the surrounding repo* — i.e. it doesn't say "the repo that hosts the standard should itself follow the standard, with these exemptions." That recursive question is exactly what this audit answers, and a paragraph in the standard formalising the answer would close the loop.

---

## 6. Recommendations (ordered by leverage)

| # | Change | Type | Leverage |
|---|--------|------|----------|
| 1 | **Reconcile "Tier 1 — no exceptions" with the cost note's friction test.** Soften the Tier 1 framing to permit narrow exemptions via DECISIONS entries. | **Standard** | Highest — fixes the contradiction that makes every meta-level self-audit incoherent and prevents future writing-style projects from feeling like they violate the standard. |
| 2 | **Add a "documentation-as-deliverable" Workflow Variation** (alongside AI-first and Research-driven) and a brief note in the README, CLAUDE, and Lifecycle specs that some required sections may be N/A for non-code projects. | **Standard** | High — once the variation exists, this repo and any future style-guide-type repo gets a clean spec to follow. |
| 3 | **Add `CLAUDE.md` to this repo** describing: main artifact, contributor workflow (refresh Provenance log + Last reviewed on material change), invariants (append-only IDs, status vocabulary), conventions (markdown style, where DECISIONS entries go), out-of-scope (no code yet). | **Repo** | High — friction test fires today; also makes the repo a worked example of its own Tier 1. |
| 4 | **Update CHANGELOG.md** to record `D-002` / `D-003` / `skeletons/` / `PROMPTS.md` — either fold into 0.1.0 (same date) or open `[Unreleased]`. | **Repo** | High — direct conflict with the standard's CHANGELOG cross-reference rule; easy fix. |
| 5 | **Update README documentation map** to include [`PROMPTS.md`](PROMPTS.md) and [`skeletons/`](skeletons/). Consider noting `development_documentation.md` plays the SPEC role. | **Repo** | High — direct conflict, easy fix. |
| 6 | **Add a recursive-application paragraph to "Evolution of this standard"** explicitly stating that the host repo follows the standard with documented exemptions. Reference this audit (or its successor) as the canonical record of those exemptions. | **Standard** | Medium — closes the recursive loop the audit exposed. |
| 7 | **Soften ATTACK_VECTORS' "Detection is not optional" rule** to permit "manual / structural review" as a valid detection method for non-automated failure modes. | **Standard** | Medium — keeps the spec usable for documentation-style projects. |
| 8 | **Refresh `development_documentation.md` Last reviewed** to 2026-05-13 (the date PROMPTS.md and D-003 landed and effectively re-touched the standard's surface). Optional — the standard wasn't textually modified, so this is judgment-call territory. | **Repo** | Low. |
| 9 | **Decide on ATTACK_VECTORS.md** for this repo's own failure modes (drift, staleness, contradiction). The friction test doesn't fire yet; revisit after the first drift incident. | **Repo, future** | Low. |
| 10 | **Decide on PROMPTS.md as a standard-blessed doc type** (Tier 3 entry vs. project-extension). | **Standard, optional** | Low — D-003 already captures the decision locally. |
| 11 | **Decide on FEATURES.md / ROADMAP.md exemptions** — either add minimal versions to remove the "Tier 1 violator" ambiguity, or wait for change #1 (standard softening) to legitimise the omissions. | **Repo, downstream of #1** | Low — currently low friction. |

---

## Notes on what this audit didn't try to do

- I did not check that every cross-reference inside `development_documentation.md` resolves — that's a tooling job (rule 6) and not requested.
- I did not audit prose quality of the standard, only its self-application.
- I did not look at whether the skeleton files exactly match the inline skeletons in the standard — that's worth doing once changes #1–#5 land, since changes to the standard will require resyncing the skeletons.
- I have not made any changes to the repo. This file is intentionally left untracked for you to review.
