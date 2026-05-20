# Changelog

All notable changes to this project will be documented in this file.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
This project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- `skeletons/` directory with eight copy-paste-ready starter files (`README`, `FEATURES`, `CLAIMS`, `DECISIONS`, `ATTACK_VECTORS`, `ROADMAP`, `CLAUDE`, `CHANGELOG`) plus a directory `README.md` explaining the copy-rename-fill workflow and tier mapping.
- `PROMPTS.md` with three narrow cold-start prompts: bootstrap a new project, audit an existing repo, revive a Dormant project.
- `CLAUDE.md` for this repo, adapted per the Documentation-as-deliverable Workflow Variation. Documents the repo's invariants, conventions, pitfalls (notably skeleton drift), and out-of-scope items.
- `.gitignore` covering `SELF_AUDIT.md`, `audit-*.md`, editor cruft, and pre-emptive Python entries for future scaffolding scripts.
- `D-002` recording the skeletons-vs-usage-guide decision.
- `D-003` recording the choice of three narrow prompts in `PROMPTS.md` over an exhaustive prompts file.
- `D-004` recording the five-edit package of standard revisions following the first self-audit.
- `D-005` recording the Tier 1 exemption for `FEATURES.md` (this repo's deliverable is a standard, not a tool with capabilities).
- `D-006` recording the Tier 1 exemption for `ROADMAP.md` (the standard is revised inline, not in phases).
- `D-007` recording the five-revision package of standard changes following the second self-audit (Arithmancy).
- `D-008` recording the addition of `BUGS.md` as a Tier 2 document type with `BUG-NNN` stable IDs and status vocabulary (open / fixed / wontfix / deferred). Format adopted from `tux-ti83`'s in-repo bug catalogue.
- `D-009` recording the addition of `IMPROVEMENTS.md` as a Tier 2 document type with `IMP-NNN` stable IDs and status vocabulary (suggested / applied / declined / deferred). The dual of BUGS.md; trade-offs are required per entry.
- `D-010` recording new Maintenance Rule 8 — "Log when found, not silently acted on" — the workflow discipline that makes BUGS.md and IMPROVEMENTS.md useful catalogues.
- **`BUGS.md` as a Tier 2 document type** in the standard, with per-document specification, file header, entry format, four maintenance rules, and worked example (BUG-019 from tux-ti83). New entry in §SDLC mapping, §Tier 2 table, §Quick Decision Guide, and reserved-names list.
- **`IMPROVEMENTS.md` as a Tier 2 document type** in the standard, with per-document specification, file header, entry format, four maintenance rules, and worked example (IMP-021 from tux-ti83). Trade-offs required per entry. New entry in §SDLC mapping, §Tier 2 table, §Quick Decision Guide, and reserved-names list.
- **Maintenance Rule 8 ("Log when found, not silently acted on")** added to §Maintenance Rules. Behavioral commitment for AI partners and human contributors when working in a project that has BUGS or IMPROVEMENTS files: log discoveries rather than silently fix or apply them; the user decides whether to act, defer, or decline.
- `skeletons/BUGS.skeleton.md` and `skeletons/IMPROVEMENTS.skeleton.md` — copy-paste-ready starter files matching the new per-document specs. Mirror the standard's §Minimal File Skeletons section.
- `audits/` directory with `2026-05-13-self-audit.md`, the diagnostic record of the first self-audit run against this repo. Kept as a dated snapshot; future audits land in the same directory with their own YYYY-MM-DD prefix.
- Documentation-as-deliverable Workflow Variation in the standard, covering the meta-level case where the project's deliverable is documentation itself. Spells out which Tier 1 documents adapt and which are legitimate exemptions.
- Recursive-application paragraph in the standard's Evolution section, explicitly stating that the host repo follows the standard with documented exemptions.
- Project-specific-extensions clause in the Evolution section, listing reserved names and the conditions under which projects may add document types beyond those the standard names.
- **Retroactive completion** subsection in the standard's §Project lifecycle, specifying the minimum acceptable path for projects that finish development without having adopted the standard during Active phase. Status header update + sealing DECISIONS entry + optional CLAIMS audit pass.
- **Future-revival friction test** in §A note on cost — forward-tense variant of the friction test triggered by Complete-state transitions, with mandatory / strongly-recommended / case-by-case threshold tiers.
- **Complete-state projects** Workflow Variation in §Creation Order, alongside AI-first, Research-driven, and Documentation-as-deliverable. Specifies the Complete-state shape of `CLAUDE.md` (Frozen state / Revival triggers / Out of scope / What to read first on revival).

### Changed
- **Tier 1 framing reconciled with the cost note.** Header changed from "Tier 1 — Always (every project, no exceptions)" to "Tier 1 — Default minimum (every project, with narrow documented exemptions)." Body text now requires Tier 1 omissions to be recorded as `DECISIONS.md` entries with reasoning. The cost note section was extended to explicitly cover Tier 1 with the same friction test plus the documented-exemption requirement. Fixes the internal contradiction identified by the first self-audit (2026-05-13).
- **ATTACK_VECTORS Maintenance Rule 4** extended. Initially softened from "Detection is not optional" to "Detection is defined, not necessarily automated" (first audit). Now further extended to three first-class detection categories: implemented automated, implemented manual, and acknowledged-but-not-implemented (`Detection: not implemented (would require X); see CLAIMS C-NNN`). An undetected vector is itself signal for Complete-state projects whose claimed verification was never operationalised.
- **DECISIONS entry format: `Date:` replaced with `Decided:` and `Recorded:` fields.** For normal entries both are identical; for retroactive entries (e.g. during retroactive completion) they diverge. Either field alone is acceptable when the other is unknown. The convention is added to the entry-format example, file-header description, and `skeletons/DECISIONS.skeleton.md`. The six existing entries in this repo's `DECISIONS.md` migrated to the new format.
- **Append-only IDs rule (Maintenance Rule 3) extended** to cover `BUG-` and `IMP-` namespaces alongside the existing `F-`, `C-`, `D-`, `AV-`.
- **CHANGELOG per-document spec extended** to reference `BUG-` and `IMP-` IDs in examples and the traceability list ("Reference F-, C-, D-, AV-, BUG-, and IMP- IDs for full traceability").
- **§SDLC mapping** gains two rows: "What went wrong (realised)?" → `BUGS.md`; "What could be better (candidate)?" → `IMPROVEMENTS.md`.
- **§Critical separations** gains two new pairings: ATTACK_VECTORS (anticipated) vs BUGS (realised); BUGS (broken) vs IMPROVEMENTS (works but could be better).
- **Skeletons index (`skeletons/README.md`) extended** with rows for BUGS.skeleton.md and IMPROVEMENTS.skeleton.md.
- **Repo `CLAUDE.md` updated** to reflect new DECISIONS entries (D-004 through D-010), the new skeleton count (10), the new `audits/` directory, the explicit Tier 2 absence reasoning for BUGS/IMPROVEMENTS, and the Maintenance Rule 8 note (moot here because neither doc exists).
- Standard's Provenance log appended with three revision entries: two 2026-05-13 (self-audit one and Arithmancy audit two) and one 2026-05-21 (BUGS/IMPROVEMENTS adoption); Last reviewed updated from 2026-05-13 to 2026-05-21.

## [0.1.0] — 2026-05-13

### Added
- Initial release of the development documentation standard (`development_documentation.md`).
- Tier 1 (always), Tier 2 (strongly recommended), and Tier 3 (conditional) document classifications.
- Stable ID conventions: `F-NNN` (features), `C-NNN` (claims), `D-NNN` (decisions), `AV-NNN` (attack vectors).
- README status header standard with five-value status vocabulary (Active / Dormant / Complete / Archived / Superseded).
- Project lifecycle transition procedures.
- Integration patterns for critic tools and AI development partners.
- Repo scaffolding: `README.md`, `LICENSE` (CC BY 4.0), `CHANGELOG.md`, `DECISIONS.md`.
- `D-001` recording the chosen standard format (tier system, stable IDs, lifecycle vocabulary).
