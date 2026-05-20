# CLAUDE.md

## Project

`project-scaffold` is the home of the Development Documentation Standard — a single normative document (`development_documentation.md`) defining the structural docs every project should carry, plus supporting material that helps users adopt it. Status: Active, first public release.

Per the standard's Documentation-as-deliverable Workflow Variation, the repo deliverable is documentation itself; there is no code, build, or test infrastructure.

## Current state

- `development_documentation.md` — the standard. Active and load-bearing. Edit only as a material revision; refresh its Provenance log inline and update its Last reviewed date.
- `README.md` — front door. Status header tracks repo state.
- `DECISIONS.md` — repo's own design log. Ten entries (D-001 standard format; D-002 skeletons directory; D-003 PROMPTS.md; D-004 standard revisions from first self-audit; D-005 / D-006 Tier 1 exemptions for FEATURES.md / ROADMAP.md; D-007 standard revisions from second self-audit (Arithmancy); D-008 BUGS.md as Tier 2; D-009 IMPROVEMENTS.md as Tier 2; D-010 Maintenance Rule 8 "Log when found, not silently acted on").
- `CHANGELOG.md` — Keep a Changelog format. `[Unreleased]` accumulates work since v0.1.0 (2026-05-13); no manual tag cut yet.
- `PROMPTS.md` — three cold-start prompts for users adopting the standard.
- `skeletons/` — ten starter files plus directory README (README, FEATURES, ROADMAP, CLAUDE, CHANGELOG at Tier 1; DECISIONS, BUGS, IMPROVEMENTS at Tier 2; CLAIMS, ATTACK_VECTORS at Tier 3). The skeleton files mirror the **Minimal File Skeletons** section of the standard and must stay in sync with it.
- `audits/` — dated diagnostic audits. Currently contains `2026-05-13-self-audit.md` (first self-audit; standard-level findings actioned via D-004; repo-level findings actioned in subsequent commits).
- `LICENSE` — CC BY 4.0. Any future code (validation scripts, scaffolding tools) will be MIT and noted in its own directory.

The repo does **not** currently have `BUGS.md` or `IMPROVEMENTS.md`. Both are Tier 2 with the friction-test override; no DECISIONS entry is required for their absence (only Tier 1 exemptions need that). Maintenance Rule 8 ("Log when found, not silently acted on") is moot here because neither document exists. If a recurring bug pattern or improvement candidate emerges, add the file rather than scattering observations into commit messages.

## Active task

No active task at present. The next likely work item is one of:

- Tagging a v0.2.0 release from `[Unreleased]` when the user is ready.
- Acting on findings from a future self-audit run (the audit prompt in `PROMPTS.md` applied to this repo).
- A material revision to the standard, triggered by drift caught during use or by a follow-up audit.
- A user-reported friction in adoption.

When working, reference any feature-equivalent IDs (D-NNN for decisions; the standard's own document types) explicitly. Acceptance criteria for any edit: the standard remains internally consistent (no contradictions between sections); the host repo follows the standard (with documented exemptions where it doesn't); cross-references between docs remain accurate.

## Invariants

These must not be violated:

- **Append-only IDs.** D-NNN entries in `DECISIONS.md` are never deleted or renumbered. Withdrawn entries get a status flag. Same rule for `F-`, `C-`, `AV-`, `BUG-`, `IMP-` if those documents are ever added.
- **Status vocabulary fidelity.** The standard's status vocabularies (project / decision / claim / bug / improvement) are fixed; do not introduce new values without a corresponding D-NNN.
- **Skeletons mirror the standard.** When the **Minimal File Skeletons** section of `development_documentation.md` changes, the corresponding `skeletons/*.skeleton.md` file must be updated to match in the same commit.
- **Self-application.** The repo follows its own standard; legitimate Tier 1 exemptions (currently `FEATURES.md` via D-005, `ROADMAP.md` via D-006) are recorded in `DECISIONS.md` and revisited if friction signals fire. Tier 2 omissions (`BUGS.md`, `IMPROVEMENTS.md`, `ARCHITECTURE.md`, `SPEC.md`, `BUILD.md`) follow the friction-test override and do not require their own DECISIONS entries.
- **Provenance log discipline.** Material revisions to `development_documentation.md` append an entry to its Provenance line and refresh its Last reviewed date.
- **Cross-references may be stale.** No tooling enforces bidirectional cross-references (per the standard's Maintenance Rule 6). Authors are responsible for keeping them current; when in doubt, search.

## Build & test

No build or test commands. This is a documentation-only repo.

Reasonable manual checks before committing a material edit:

```bash
# Render markdown locally if helpful
grip README.md      # or any other markdown viewer

# Search for references to renamed or moved sections
grep -rn "section name" .

# Confirm DECISIONS IDs remain sequential and unique
grep -n "^### D-" DECISIONS.md
```

## Conventions

- **Markdown style.** Prose paragraphs over bullet lists for explanation; bullets for enumerable items. Code fences for shell commands and skeleton excerpts. ATX-style headers (`#`, `##`, `###`).
- **DECISIONS entries** follow the format in the standard's §Per-Document Specifications → `DECISIONS.md`. Every entry must include reversal conditions; an entry without one is a belief, not a decision.
- **CHANGELOG entries** reference D-NNN IDs for traceability.
- **Commit messages.** Imperative mood, short summary line, followed by a paragraph if the change is non-trivial. Reference D-NNN in the body when applicable.
- **Dates** in ISO 8601 (YYYY-MM-DD).
- **Cross-references** within the repo use relative markdown links (e.g. `[Decisions](DECISIONS.md)`).

## Pitfalls

- The standard's `ATTACK_VECTORS.md` section is the canonical list of failure modes for projects using the standard. This repo does not have its own `ATTACK_VECTORS.md` yet (no drift incidents to date), but the standard's known failure modes apply meta-recursively to this repo too: skeleton drift, Provenance log staleness, status vocabulary drift, cross-reference rot.
- **Skeleton drift** is the most likely real failure mode. When editing the **Minimal File Skeletons** section of the standard, the matching `skeletons/*.skeleton.md` file in the directory must be updated in the same commit. Forgetting this produces silent divergence. Known existing drift: `skeletons/ATTACK_VECTORS.skeleton.md` still says "Detection is not optional", but D-007 softened the standard to three detection categories including "not implemented." That skeleton needs updating; flagged as a candidate cleanup, not currently load-bearing.
- **Retroactive CHANGELOG modification.** The standard treats version history as append-only. Once a release is tagged (v0.1.0 etc.), do not modify its CHANGELOG entry. Add new entries under `[Unreleased]` or the next version, not the released one.
- **The standard prescribes tooling it does not provide.** Maintenance Rule 6 names a cross-reference checker as illustrative, not as part of this repo's deliverables. Do not silently add such tooling here without a D-NNN entry deciding where the reference implementation belongs.
- **Maintenance Rule 8 is moot here.** This repo has no `BUGS.md` or `IMPROVEMENTS.md`. If you add either, the "log when found, not silently acted on" rule becomes load-bearing — log bug discoveries and improvement candidates rather than fixing or applying inline.

## Out of scope

The AI partner should not change these without asking:

- The choice of license (CC BY 4.0 for documentation; future MIT for code).
- The repo's overall organisation (root-level docs + `skeletons/` directory). Reorganisations are D-NNN decisions.
- The standard's stable IDs and append-only conventions — these are load-bearing for backward compatibility.
- The reserved document names listed in the standard's project-specific-extensions clause.
- This `CLAUDE.md` file's structure — refresh its content, but don't reorder its sections without a D-NNN entry.
