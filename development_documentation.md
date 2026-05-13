> **Status:** Active
> **Provenance:** Claude (initial 2026-05-07; revised 2026-05-12 adding DECISIONS.md, ATTACK_VECTORS.md, CLAIMS.md formalisation, project lifecycle, tooling integration, cost framing; revised 2026-05-12 tightening tooling integration, harmonising Authors/Provenance distinction, marking tooling references as illustrative, adding standard self-evolution rule)
> **Last reviewed:** 2026-05-12
> **Why this status:** Living standard for project documentation. Refresh as conventions evolve.

# Development Documentation Standard

This document defines the **core set of development docs** that should exist in every project, regardless of language or domain. Drop this file into a chat session to give Claude (or any collaborator) the documentation conventions to follow.

Every project also requires its own domain-specific documentation (e.g. physics derivations, protocol specs, file format references). This standard covers only the **structural / process** documents — the scaffolding that lets a project be picked up months later without losing context.

The standard is designed to serve two audiences simultaneously: humans picking the project up after a gap, and tooling (critic tools such as Crucible, AI development partners such as Claude Code) reading the project to act on it. The conventions are chosen so that the same docs work for both — humans get readable prose with structure; tools get stable IDs, fixed status vocabulary, and a known schema.

---

## How This Maps to the Software Development Lifecycle

Industry-standard SDLC phases (planning → requirements → design → implementation → testing → deployment → maintenance) each have characteristic documents. Distilled, the canonical hierarchy is:

| Question | Industry name | This standard |
|----------|--------------|---------------|
| **Why** does this project exist? | BRD (Business Requirements) | `README.md` (vision paragraph) |
| **What** does the tool/system do? | PRD (Product Requirements) | `FEATURES.md` |
| **What** does the research assert? | Claims register | `CLAIMS.md` |
| **When** will each part be built? | Roadmap / Backlog | `ROADMAP.md` |
| **How** is it structured (high level)? | SDD / Architecture Doc | `ARCHITECTURE.md` |
| **Why** were the structural choices made? | ADR log | `DECISIONS.md` |
| **How** does it work (technical detail)? | SRS / TSD | `SPEC.md` (or domain-named) |
| **How** could it break? | Threat model / failure-mode list | `ATTACK_VECTORS.md` |
| **How** do I build it? | Build/Deploy Guide | `BUILD.md` |
| **What changed and when?** | Release notes | `CHANGELOG.md` |
| **How does an AI pick this up?** | (No industry equivalent) | `CLAUDE.md` |

The critical separations:

- **Features (capabilities)** vs **Claims (assertions about the world)** — features describe what the tool does (acceptance criteria); claims describe what the research asserts is true (falsification conditions). Research-software hybrid projects need both.
- **Features (what)** vs **Spec (how)** — features are user-facing capabilities; spec is internal implementation detail.
- **Architecture (structure)** vs **Decisions (rationale)** — ARCHITECTURE describes the system as it is; DECISIONS records why it ended up that way and what alternatives were rejected.
- **Spec (correctness contract)** vs **Attack Vectors (failure modes)** — SPEC says what the system does when working; ATTACK_VECTORS lists how it can fail.

---

## Document Tiers

### Tier 1 — Always (every project, no exceptions)

| File | Purpose | SDLC phase |
|------|---------|-----------|
| `README.md` | Entry point. What the project is, status, how to build/run. | Planning |
| `FEATURES.md` | Capability list with priorities and acceptance criteria. | Requirements |
| `ROADMAP.md` | Phased development plan with explicit milestones. | Planning |
| `CLAUDE.md` | Handoff document for Claude Code / AI development sessions. | Implementation (continuous) |
| `CHANGELOG.md` | Version history; what changed and when. | Implementation (continuous) |
| `LICENSE` | Legal terms. Pick one before first public commit. | Planning |

### Tier 2 — Strongly recommended (most non-trivial projects)

| File | Purpose | SDLC phase |
|------|---------|-----------|
| `ARCHITECTURE.md` | Module boundaries, data flow, key invariants. | Design |
| `DECISIONS.md` | Indexed log of design decisions with rationale and reversal conditions. | Design (continuous) |
| `SPEC.md` (or domain-named, e.g. `PHYSICS.md`, `PROTOCOL.md`) | Authoritative technical specification. | Design |
| `BUILD.md` | Environment setup, toolchain versions, build commands. | Implementation |

### Tier 3 — Conditional (use when applicable)

| File | When to include |
|------|-----------------|
| `CLAIMS.md` | **Required for research projects** making empirical or theoretical assertions. Optional otherwise. Pairs with `FEATURES.md` for research-software hybrid projects. |
| `ATTACK_VECTORS.md` | Project has well-defined failure modes worth enumerating (physics validity, performance budgets, security, correctness). Most valuable when paired with a critic tool (e.g. Crucible). |
| `VOCABULARY.md` | When the project shares a contract with a sibling project (terms, types, IDs that must match). |
| `TESTING.md` | When test strategy is non-obvious or spans multiple harnesses. |
| `SECURITY.md` | Security-sensitive projects, or any repo accepting vulnerability reports. |
| `CONTRIBUTING.md` | Public repos accepting external contributions. |
| `CITATION.cff` / `CITATION.md` | Research code intended to be cited in publications. |
| `BENCHMARKS.md` | Performance-critical projects; record baseline numbers and methodology. |

---

## Creation Order (which doc first?)

Documents are not independent. They feed each other. The recommended order for a new project:

1. **`README.md`** (skeleton) — captures the vision paragraph and status. Even one sentence is enough to start.
2. **`FEATURES.md`** — list capabilities before designing anything. If you can't list what it does, you don't yet know what to build.
3. **`ROADMAP.md`** — group features into phases. Forces realism about scope and ordering.
4. **`ARCHITECTURE.md`** — high-level structure that can deliver the Phase 1 features.
5. **`DECISIONS.md`** — initialised alongside ARCHITECTURE.md with the first major design choices logged as D-001, D-002…
6. **`SPEC.md`** — technical detail follows architecture. Constants, formats, equations.
7. **`ATTACK_VECTORS.md`** — added when the first failure mode is identified (often during SPEC drafting or first review).
8. **`BUILD.md`** — written when the first build succeeds, captured immediately so it isn't lost.
9. **`CLAUDE.md`** — created at the start of the first AI-assisted coding session.
10. **`CHANGELOG.md`** — initialised with the first commit, appended continuously.
11. **`LICENSE`** — before first public commit.

Tier 3 documents are added when their trigger condition fires (see the Quick Decision Guide at the end).

### Workflow variations

**AI-first projects.** When Claude Code (or another AI coding partner) is the primary development environment from the start, create `CLAUDE.md` at step 2, immediately after `README.md`, so the AI partner has project state to read from day one. The remaining conceptual order is unchanged.

**Research-driven projects.** When the project is primarily research with code as a deliverable (e.g. a theoretical physics paper with accompanying simulation code), create `CLAIMS.md` at step 2 or 3, before or alongside `FEATURES.md`. The claims define what the code must demonstrate; features then describe the tooling required to test the claims. `ARCHITECTURE.md` and `SPEC.md` may also start earlier than usual, since the mathematical framework often precedes the code.

**Rule of thumb:** if you find yourself writing code before `FEATURES.md` (or `CLAIMS.md`, for research) exists, stop. You're guessing at scope rather than defining it.

---

## The README Status Header Standard

Every `README.md` begins with a four-line blockquote header:

```markdown
> **Status:** {Active | Dormant | Complete | Archived | Superseded}
> **Provenance:** {role tags — e.g. "Claude (primary auditor)", "Gemini (early scaffolding)"}
> **Last reviewed:** YYYY-MM-DD
> **Why this status:** {cause, forward intent, or resumption condition}
```

**Status vocabulary (use exactly these words):**

- **Active** — under current development; commits expected within weeks.
- **Dormant** — paused but intended to resume. The "Why" line states the resumption condition.
- **Complete** — feature-complete and stable. No further work planned, but bug fixes possible.
- **Archived** — abandoned or read-only. Not maintained.
- **Superseded** — replaced by another project. The "Why" line names the successor.

The transitions between these states have their own discipline — see **Project lifecycle** below.

---

## Per-Document Specifications

### `README.md`

The front door. Optimised for someone who has never seen the project before.

**Required sections (in order):**

1. **Status header** (the blockquote above).
2. **One-paragraph description** — what the project is, who it's for, what makes it distinctive.
3. **Quick start** — the shortest path from clone to running output. Real commands, not prose.
4. **Build requirements** — toolchain, OS targets, key dependencies with versions. Link to `BUILD.md` if non-trivial.
5. **Project structure** — top-level directory tree with one-line annotations.
6. **Documentation map** — links to `FEATURES.md`, `ARCHITECTURE.md`, `DECISIONS.md`, `ROADMAP.md`, `SPEC.md`, `ATTACK_VECTORS.md`, `CLAIMS.md` as applicable.
7. **License** — one line stating the license and linking to `LICENSE`.

### `FEATURES.md`

The **what**, not the how. Lists every capability the project offers (or intends to offer), prioritised, with acceptance criteria.

**Required sections:**

1. **Target users** — who this is for, in one or two sentences.
2. **Feature list** — grouped by area, each with priority and acceptance criteria.
3. **Out of scope** — explicit list of things this project will not do.
4. **Future / candidate features** — ideas not committed to.

**MoSCoW priorities:** Must / Should / Could / Won't.

**Feature entry format:**

```markdown
### F-012 Procedural hovercraft physics
**Priority:** Must
**Acceptance:**
- Hovercraft responds to thrust, yaw, pitch inputs at 120 Hz fixed timestep
- Four flight-assist levels selectable at runtime
**Status:** Complete (Phase 2)
**Notes:** See ARCHITECTURE.md §Physics for integration scheme.
```

Stable IDs (`F-012`) let `ROADMAP.md`, `CHANGELOG.md`, `DECISIONS.md`, and commit messages reference features unambiguously. IDs are append-only; withdrawn features get `Status: Withdrawn` rather than being deleted.

**Relationship to `CLAIMS.md`:** for research-software hybrid projects (most theoretical work with accompanying code), `FEATURES.md` and `CLAIMS.md` are both required. They cover orthogonal axes:

- `FEATURES.md` describes what the tool/system *does*, checked by **acceptance criteria** (tests, code execution).
- `CLAIMS.md` describes what the research *asserts is true*, checked by **falsification conditions** (data, proof, observation).

A worked example: for a modified-gravity paper with accompanying simulation code, FEATURES covers "test suite must pass 38/38", "SPARC analysis script runs end-to-end", "LaTeX builds cleanly"; CLAIMS covers "the free function predicts a sign-reversal observable at angle θ≈8.5 arcmin in Euclid Wide Survey data". The first set is engineering deliverables; the second is scientific commitments. Pure code projects with no scientific claims need only FEATURES. Pure research notes with no code may need only CLAIMS.

### `CLAIMS.md`

The research counterpart to `FEATURES.md`. Lists every empirical, theoretical, or mathematical assertion the project makes, with the conditions under which each would be considered refuted.

**Required sections:**

1. **Scope** — what kinds of claims this document covers (empirical predictions, mathematical proofs, theoretical derivations).
2. **Claims list** — grouped by domain or paper section, each with status and falsification conditions.
3. **Withdrawn / refuted claims** — claims that did not survive review, kept for audit trail.

**Status vocabulary:** Proposed | Supported | Refuted | Withdrawn.

**Claim entry format:**

```markdown
### C-003 Gravitational wave speed compatibility
**Status:** Supported
**Domain:** Empirical
**Authors:** Shane Hartley (with Crucible review 2026-03-15)
**Related:** F-027 (test_gw_speed.py), D-004 (mimetic conformal framing), AV-003

**Statement.** The scalar-tensor sector preserves c_GW = c at λ = 0 to within the GW170817 bound |c_GW/c − 1| < 5×10⁻¹⁶.

**Falsification conditions.** Either (a) symbolic derivation in `derivations/causality.ipynb` produces a non-zero coefficient on the (∂ϕ)² gradient term at λ = 0, or (b) any future multimessenger event tightens the GW170817 bound by ≥1 order of magnitude and the prediction fails it.

**Current evidence.** 38/38 unit tests pass; LAM_BOUNDS tightened to 0.35 after V4.2 review found marginal violation at λ = 0.44.

**Reversal conditions.** Refuted if either falsification condition fires.
```

Stable IDs (`C-001`, `C-002`, …) let papers, commits, and DECISIONS entries reference claims unambiguously. IDs are append-only; refuted or withdrawn claims keep their IDs and gain a status flag.

**Maintenance rules:**

1. **Falsification conditions are not optional.** A claim without a falsification condition is a belief, not a claim. Reviewers (human or Crucible) should reject entries that fail this.
2. **Status changes get a DECISIONS entry.** Moving a claim from Supported to Refuted is a significant project event and must be logged.
3. **Cite from papers.** Published or preprinted work referencing the project should cite by claim ID, so reviewers can trace the source of any specific assertion.

### `ARCHITECTURE.md`

The structural document. With `DECISIONS.md` carrying rationale, ARCHITECTURE.md is purely descriptive — it describes the system as it currently is.

**Recommended sections:**

1. **System overview** — diagram or ASCII art showing module boundaries and data flow.
2. **Module responsibilities** — one paragraph per top-level module.
3. **Key invariants** — rules the system must maintain.
4. **Cross-cutting concerns** — logging, error handling, concurrency model, threading model.

The "why did we do it this way" content lives in `DECISIONS.md`, not here. ARCHITECTURE describes; DECISIONS justifies.

### `DECISIONS.md`

The indexed log of design decisions. Each entry captures what was decided, what alternatives were considered, why this option was chosen, and what evidence would reverse it. It is the audit trail that survives six-month gaps in attention.

This is the project's ADR (Architecture Decision Record) log. When a critic tool such as Crucible is part of the workflow, sealed conclusions from review sessions are recorded here — Crucible suggests entries; the author adjudicates and merges. Without Crucible, the author writes entries directly; the structural role is identical.

**File header:**

```markdown
# Decisions

Append-only log of significant design decisions.
Each entry: D-NNN, dated ISO 8601, with status, context, alternatives, decision, consequences, and reversal conditions.
Status vocabulary: Proposed | Accepted | Superseded by D-NNN | Deprecated.
```

**Entry format:**

```markdown
### D-007 Fixed 120 Hz physics timestep
**Date:** 2026-03-14
**Status:** Accepted
**Authors:** Shane Hartley (with Crucible review 2026-03-15)
**Related:** F-012, F-018, SPEC.md §Physics

**Context.** terra-siege physics needs deterministic replay and stable integration for a hovercraft with aggressive control inputs near terrain. Three options were considered.

**Options.**
- **A. Variable timestep tied to frame rate.** Simplest. Rejected: non-determinism breaks replay; integration instability at low frame rates.
- **B. Fixed 60 Hz timestep with interpolated rendering.** Standard game-physics pattern. Considered but rejected for this project — proportional-navigation missile guidance shows visible jitter at 60 Hz.
- **C. Fixed 120 Hz timestep with interpolated rendering.** Chosen.

**Decision.** Option C. Physics steps at 120 Hz regardless of frame rate; rendering interpolates between the two most recent physics states.

**Consequences.**
- Replay determinism guaranteed if inputs are recorded at physics-tick granularity.
- ~2× physics CPU vs 60 Hz baseline. Measured 0.4 ms/tick on target hardware; budget is 8 ms.
- Missile guidance and ground-effect controllers can use tighter loop gains.

**Reversal conditions.** Revisit if (a) physics cost exceeds 30% of frame budget on minimum-spec hardware, or (b) replay determinism is no longer a requirement.
```

**Maintenance rules:**

1. **Append-only.** Decisions are never deleted. When a decision is reversed, write a new entry with `Status: Accepted` and update the old entry to `Status: Superseded by D-NNN`.
2. **Stable IDs.** `D-001`, `D-002`, … sequentially. Referenced from commits, CHANGELOG entries, and other documents.
3. **One decision per entry.** If a session produces three sealed conclusions, that's three entries.
4. **Reversal conditions are not optional.** Every entry must state what evidence would change the decision. A decision without a reversal condition is a belief, not a decision.

### `SPEC.md` (or domain-specific spec)

The authoritative technical reference. For a game: physics constants, input mappings, save format. For a protocol: message types, state machines. For a research framework: equations, parameters, observable predictions.

Use the name that fits the domain (`PROTOCOL.md`, `FORMAT.md`, `PHYSICS.md`).

**Distinction from `FEATURES.md`:** a feature says "the hovercraft has four flight-assist levels." The spec says "Assist level 3 applies PD controller gains Kp=4.2, Kd=0.8 to roll axis."

### `ATTACK_VECTORS.md`

The project-specific failure-mode checklist. Lists the ways this particular system can be wrong, broken, or compromised — distinct from generic security or testing concerns.

This is where domain knowledge about *how things go wrong* is captured so it can be checked routinely rather than rediscovered after a regression. When a critic tool such as Crucible is in use, this document is co-authored: Crucible proposes additions when it discovers a new failure mode during review; the author adjudicates and merges. Without Crucible, the author maintains it directly from review and post-mortem activity.

**Distinction from `TESTING.md`:** ATTACK_VECTORS lists *what to check*; TESTING describes *how the test infrastructure is organised*. ATTACK_VECTORS entries often correspond to test cases, but the document is the canonical list of concerns, not the test inventory.

**Distinction from `SECURITY.md`:** ATTACK_VECTORS covers all failure modes (correctness, performance, numerical stability, domain validity); SECURITY is specifically about adversarial threats and reporting policy. For a physics project, ATTACK_VECTORS is the right home for "GW170817 constraint violation" — it isn't a security issue, it's a domain failure mode.

**File header:**

```markdown
# Attack Vectors

Project-specific failure modes the project must be resilient against.
Grouped by category. Each vector lists detection method and severity.
Severity: Critical (must hold) | Major (regression on release blocks) | Minor (track only).
```

**Entry format:**

```markdown
## Physics validity

### AV-003 Gravitational wave speed deviation
**Severity:** Critical
**Description.** Any modification to the scalar-tensor sector must preserve c_GW = c at λ = 0 to within the GW170817 bound |c_GW/c - 1| < 5×10⁻¹⁶.
**Detection.** `tests/test_gw_speed.py::test_gw170817_bound`. Symbolic check in `derivations/causality.ipynb`.
**Related decisions.** D-004 (mimetic conformal framing), D-012 (LAM_BOUNDS = 0.35 ceiling).
**Related claims.** C-003.
**History.** Re-tightened to λ ≤ 0.35 after V4.2 review found marginal violation at λ = 0.44.

## Numerical stability

### AV-007 Hot-path heap allocation
**Severity:** Major
**Description.** No allocations inside `Physics::step()` or `Renderer::draw()`. Allocator pressure causes frame-time spikes that violate the 8 ms physics budget.
**Detection.** AddressSanitizer with allocation hook on hot paths; `tools/check_allocs.sh`.
**Related decisions.** D-007 (fixed 120 Hz timestep), D-015 (pre-sized object pools).
```

**Maintenance rules:**

1. **Stable IDs.** `AV-001`, `AV-002`, …, append-only. Referenced from tests, commits, and DECISIONS entries.
2. **Co-authored when a critic tool is in use.** Crucible (or equivalent) suggests; the author adjudicates. Without such a tool, the author maintains it from review activity.
3. **Cross-reference both directions.** ATTACK_VECTORS entries name the related DECISIONS and CLAIMS; those documents reference back. (See Maintenance Rules below for tooling.)
4. **Detection is not optional.** Every vector must state how it is checked. A vector without a detection method is a worry, not a vector.

### `BUILD.md`

1. **Supported platforms** — OS, architecture, toolchain versions.
2. **Dependencies** — exact versions, install commands per platform.
3. **Build commands** — debug, release, test, package.
4. **Cross-compilation** — if applicable.
5. **Troubleshooting** — known build failures and fixes.

### `CLAUDE.md`

The handoff document for AI-assisted development sessions.

**Required sections:**

1. **Project summary** — 2–3 sentences.
2. **Current state** — what works, what's stubbed, what's broken. File-level specificity.
3. **Active task / next milestone** — immediate work item with acceptance criteria. Reference feature IDs.
4. **Architectural invariants** — rules that must not be violated.
5. **Build & test commands** — exact commands to verify changes.
6. **Conventions** — naming, formatting, comment style, commit message format.
7. **Known pitfalls** — non-obvious traps. May reference `ATTACK_VECTORS.md` for the canonical list.
8. **Out of scope** — explicit list of things the AI should not change without asking.

Refresh `CLAUDE.md` at the end of every significant session. Current state, not history.

### `ROADMAP.md`

```markdown
## Phase 1 — {Phase name}
**Goal:** {one sentence}
**Status:** {Not started | In progress | Complete}
**Features delivered:** F-001, F-003, F-007
**Deliverables:**
- [ ] {item with file/module reference}
**Acceptance:** {how we know this phase is done}
```

Phases are append-only; mark Complete with an ISO date.

### `CHANGELOG.md`

Follow [Keep a Changelog](https://keepachangelog.com).

```markdown
## [Unreleased]
### Added
- F-014 ego-centric radar with altitude strip
### Changed
- D-007 confirmed under load testing (no reversal triggered)
### Fixed
- AV-007: removed stray std::vector growth in Physics::step()
```

Reference F-, C-, D-, and AV- IDs for full traceability.

### Other Tier 3 docs

- **`VOCABULARY.md`** — shared contract with a sibling project; single source of truth.
- **`TESTING.md`** — test pyramid, harness setup, fixture conventions, how to add a new test.
- **`SECURITY.md`** — threat model, reporting policy, supported versions.
- **`CONTRIBUTING.md`** — branch model, PR checklist, review expectations, code style.
- **`BENCHMARKS.md`** — methodology, hardware, baseline numbers, regression policy.

---

## Integration with tooling

This standard is designed so the same documents serve both humans and tooling. The interface contract is summarised here; detailed protocols for specific tools (Crucible, Cairn, Claude Code) belong in those tools' own documentation as they mature.

**For critic tools** (review, stress-test assumptions, identify failure modes): READ from `FEATURES.md` / `CLAIMS.md` (gates), `ARCHITECTURE.md` (invariants to attack), `DECISIONS.md` (do not re-litigate Accepted decisions unless reversal conditions are met), `SPEC.md` (symbolic ground truth), `ATTACK_VECTORS.md` (do not duplicate known vectors). WRITE proposed entries into `DECISIONS.md`, `ATTACK_VECTORS.md`, or suggested status transitions on `CLAIMS.md` / `FEATURES.md`. All writes require author adjudication.

**For AI development partners** (act on the active task): READ `CLAUDE.md` first as the contract, then other docs as needed. The properties of this standard that matter most to AI partners are stable IDs, fixed status vocabularies, reversal/falsification conditions as triggers for revisiting commitments, and append-only history. If an AI partner is also acting as a critic, it writes into the structured docs (DECISIONS, ATTACK_VECTORS) rather than scattering observations across `CLAUDE.md`.

**Provenance fields are parallel but distinct.** Use the same role-tag vocabulary (e.g. "Crucible", "Claude (review)", "Gemini (scaffolding)") in both, but the fields mean different things:

- `README.md` **Provenance** is project-scoped: who/what contributes to the project overall. Format: list of role-tagged contributors. Updated when the contributor mix changes.
- `DECISIONS.md` / `CLAIMS.md` **Authors** is entry-scoped: who made this specific decision or claim, and which tools reviewed it. Format: primary author (with reviewers and dates if applicable). Set when the entry is written.

A reader looking at "who built this project" reads Provenance; a reader looking at "who decided this" reads Authors on the entry.

This integration section is deliberately brief — a fuller specification, including the combined-workflow dataflow, lives with Crucible's own documentation when that tool is built. The standard reserves the slots (entry formats with Authors lines, fixed status vocabularies, append-only IDs); the protocol details that operate over those slots are versioned with the tool, not with this document.

---

## Maintenance Rules

1. **Status header refresh.** Whenever you open a project after >2 weeks away, update `README.md`'s Last reviewed date and Status if drifted.
2. **CLAUDE.md is current state, not history.** Rewrite when state changes; don't append.
3. **Append-only IDs.** FEATURES (F-), CLAIMS (C-), DECISIONS (D-), ATTACK_VECTORS (AV-) all use append-only sequential IDs. Withdrawn/superseded entries get a status flag, never deletion — outside references may still point at them.
4. **ROADMAP phases are append-only.** Mark complete, don't delete.
5. **One source of truth per fact.** A constant defined in `SPEC.md` should not be duplicated in `README.md`. Link instead.
6. **Cross-references both directions, with tooling.** When DECISIONS-N cites ATTACK-VECTOR-M, ATTACK-VECTOR-M should cite DECISIONS-N back. Same for FEATURES ↔ DECISIONS, CLAIMS ↔ DECISIONS, and CLAIMS ↔ ATTACK_VECTORS where applicable. This rule decays without enforcement: a pre-commit hook walking all docs, building the cross-reference graph, and reporting broken or unidirectional links is the canonical fix (a `tools/check_xrefs.py` script is one illustrative implementation, not part of this standard). Without such tooling, treat the rule as aspirational rather than enforced — and acknowledge in `CLAUDE.md` that cross-references may be stale.
7. **Docs are part of the commit.** A code change that invalidates documentation but doesn't update it is an incomplete commit.

### Evolution of this standard

This document is itself subject to its own rules. Material changes are logged inline in the Provenance line of the status header with a date and short description (e.g. "revised 2026-05-12 adding DECISIONS.md, ATTACK_VECTORS.md, CLAIMS.md formalisation"). The status header's Last reviewed date is updated on every material change.

When the standard reaches sufficient complexity to warrant it — multiple contributors, contested changes, or formal versioning needs — it becomes a project in its own right with its own `DECISIONS.md` recording the rationale for each material revision and what alternatives were rejected. Until then, the inline Provenance log in the header is the audit trail.

Backward compatibility is preserved by the append-only ID rule: no revision of this standard removes or renumbers a document type. New document types may be added (as CLAIMS.md was in the 2026-05-12 revision), but `D-007` in any project always means the same entry it did when written.

---

## Project lifecycle

Projects don't only get created; they transition between states. The five Status values (Active, Dormant, Complete, Archived, Superseded) only carry meaning if transitions are recorded. Without explicit procedure, status drift goes unmarked and audit trails break.

### Transitions

**Active → Dormant.** Paused with intent to resume.

- Update `README.md` header: Status, Last reviewed, Why (state the resumption condition explicitly).
- Add a `DECISIONS.md` entry recording the pause: context, resumption trigger, what state was captured.
- Ensure `CLAUDE.md` reflects current state, not aspirations. If the AI partner would be misled by stale content, rewrite it.
- If using Cairn or equivalent session-state tooling, seal a capsule at the pause point.

**Dormant → Active.** Resumption.

- Update `README.md` header (Status, Last reviewed, Why).
- Add a `DECISIONS.md` entry noting the resumption and any context shift since the pause (priorities changed, prior assumption invalidated by external work, etc.).
- Refresh `CLAUDE.md` from the resumption point. Treat it as a new handoff, not a continuation.

**Active → Complete.** Feature-complete and stable.

- All `FEATURES.md` Must-priority entries marked Complete or explicitly Withdrawn.
- All `CLAIMS.md` entries have current status recorded (Supported / Refuted / Withdrawn).
- Final `DECISIONS.md` entry sealing the completion: scope as delivered vs scope as planned, known limitations, expected maintenance posture.
- Update `ROADMAP.md` to mark all phases Complete (with ISO dates) or explicitly Withdrawn.

**Active or Complete → Archived.** Abandoned or read-only.

- Update `README.md` header: Why line must state the reason (superseded, no longer relevant, technical debt overwhelming, lost interest).
- Final `DECISIONS.md` entry: archival decision with context.
- Audit other projects' docs for references; update or mark stale. (If A is archived and B references A, B's CLAUDE.md or relevant doc should note that A is no longer maintained.)

**Any → Superseded.** Replaced by another project.

- Update `README.md` header: Why line names the successor (link if internal).
- The successor's `README.md` should reference the predecessor.
- Final `DECISIONS.md` entry recording the succession and any lessons or assets carried over.
- For research projects, `CLAIMS.md` entries should be ported to the successor (with new IDs) or formally retired with the reason recorded.

### Why this matters

A project that drifts to Dormant without documentation looks identical to an Active project from the outside — same files, same README claiming work in progress. When you return six months later, you can't reconstruct where you stopped or why. The transition discipline ensures the documents tell the truth about the project's state regardless of how long ago the last commit was.

For projects shared with collaborators, AI partners, or future-you, this is the difference between resuming work in an hour and losing a day to archaeology.

---

## Minimal File Skeletons

### `README.md` skeleton

````markdown
> **Status:** Active
> **Provenance:** {your name} (initial commit, YYYY-MM-DD)
> **Last reviewed:** YYYY-MM-DD
> **Why this status:** Initial scaffolding.

# {Project Name}

{One-paragraph description.}

## Quick Start

```bash
{exact commands}
```

## Documentation

- [Features](FEATURES.md)
- [Claims](CLAIMS.md)  <!-- research projects only -->
- [Architecture](ARCHITECTURE.md)
- [Decisions](DECISIONS.md)
- [Roadmap](ROADMAP.md)
- [Build instructions](BUILD.md)
- [Changelog](CHANGELOG.md)

## License

{License name} — see [LICENSE](LICENSE).
````

### `FEATURES.md` skeleton

```markdown
# Features

## Target users
{One or two sentences.}

## Out of scope
- {explicit non-goal}

## Features

### F-001 {Feature name}
**Priority:** Must
**Acceptance:**
- {measurable condition}
**Status:** {Not started | In progress | Complete | Withdrawn}

## Candidate features (uncommitted)
- {idea worth tracking}
```

### `CLAIMS.md` skeleton

```markdown
# Claims

Empirical, theoretical, or mathematical assertions made by this project, with falsification conditions.

Status vocabulary: Proposed | Supported | Refuted | Withdrawn.

## Scope
{What kinds of claims this document covers.}

## Claims

### C-001 {Claim title}
**Status:** Proposed
**Domain:** {Empirical | Theoretical | Mathematical}
**Authors:** {author} (with {critic tool} review {date} if applicable)
**Related:** F-NNN, D-NNN, AV-NNN

**Statement.** {The claim, precise enough to be falsifiable.}

**Falsification conditions.** {What evidence or proof would refute this claim.}

**Current evidence.** {Tests passed, papers cited, datasets analysed.}

**Reversal conditions.** {What would move this claim to Refuted or Withdrawn.}

## Withdrawn / refuted claims
{Kept for audit trail.}
```

### `DECISIONS.md` skeleton

```markdown
# Decisions

Append-only log. Status: Proposed | Accepted | Superseded by D-NNN | Deprecated.

### D-001 {Decision title}
**Date:** YYYY-MM-DD
**Status:** Accepted
**Authors:** {author} (with {critic tool} review {date} if applicable)
**Related:** F-NNN, C-NNN, AV-NNN

**Context.** {Why this decision was needed.}

**Options.**
- **A. {Option}.** {Why rejected or chosen.}
- **B. {Option}.** {Why rejected or chosen.}

**Decision.** {Chosen option, restated.}

**Consequences.**
- {Implication.}

**Reversal conditions.** {What evidence would change this decision.}
```

### `ATTACK_VECTORS.md` skeleton

```markdown
# Attack Vectors

Project-specific failure modes. Severity: Critical | Major | Minor.

## {Category}

### AV-001 {Vector title}
**Severity:** Critical
**Description.** {What can go wrong.}
**Detection.** {How it is checked — test path, tool, manual review.}
**Related decisions.** D-NNN
**Related claims.** C-NNN
**History.** {When/how this vector was identified, prior incidents.}
```

### `CLAUDE.md` skeleton

````markdown
# CLAUDE.md

## Project
{2–3 sentences.}

## Current state
- {file/module}: {status}

## Active task
{Immediate next work item. Reference feature IDs.}

## Invariants
- {rule that must hold}

## Build & test
```bash
{commands}
```

## Conventions
- {naming, style, commit format}

## Pitfalls
- See ATTACK_VECTORS.md for the canonical list.
- {session-specific gotcha}

## Out of scope
- {do not change without asking}
````

### `ROADMAP.md` skeleton

```markdown
# Roadmap

## Phase 1 — Foundation
**Goal:** {one sentence}
**Status:** In progress
**Features delivered:** F-001, F-002
**Deliverables:**
- [ ] {item}
**Acceptance:** {criterion}
```

### `CHANGELOG.md` skeleton

```markdown
# Changelog

Format follows [Keep a Changelog](https://keepachangelog.com).

## [Unreleased]
### Added
- Initial scaffolding.
```

---

## A note on cost

Documentation is not free. Every doc added is a doc that must be maintained, kept consistent with the code, and refreshed as understanding evolves. Stale docs are worse than missing docs because they actively mislead — a reader who finds no document knows they have to ask; a reader who finds an outdated document acts on bad information.

The Quick Decision Guide below leans towards adding documents because the absence of a needed doc usually costs more than the maintenance burden of a present one — but this is a default, not a rule. Skip a Tier 2 or Tier 3 doc when:

- The project is small enough that the README plus code comments capture everything (toy scripts, single-file utilities, throwaway experiments).
- A specific doc's content is genuinely covered by another (e.g. `ARCHITECTURE.md` may be unnecessary for a single-file project; `DECISIONS.md` may be unnecessary if no significant choices were made).
- Maintenance burden would exceed signal value (don't write a CHANGELOG for a project no one else will ever read; don't write CLAIMS for code that makes no scientific assertions).

The operational test is **friction**: are you currently or recently confused about something the absent doc would have answered? If yes, add it. If no, the absence isn't costing you anything yet. Adding documents pre-emptively against confusion that never arrives is itself a form of waste.

The Tier 1 set is the minimum below which projects reliably suffer. Tier 2 and Tier 3 are case-by-case.

---

## Quick Decision Guide

When starting a new project, ask:

1. Will I (or anyone else) need to pick this up after >1 month away? → **Tier 1 mandatory.**
2. More than one or two non-trivial design choices expected? → Add **`DECISIONS.md`** from day one.
3. Does the build involve more than one command, or non-trivial dependencies? → Add **`BUILD.md`**.
4. Are there >3 modules or non-obvious design decisions? → Add **`ARCHITECTURE.md`**.
5. Is there a formal spec (file format, protocol, equations, parameters)? → Add **`SPEC.md`** (or domain name).
6. Does the project have well-defined failure modes (physics validity, performance budgets, numerical stability, correctness invariants)? → Add **`ATTACK_VECTORS.md`**.
7. Is this a research project with empirical, theoretical, or mathematical claims? → Add **`CLAIMS.md`** (effectively mandatory for research).
8. Does this project share terms/types with a sibling repo? → Add **`VOCABULARY.md`**.
9. Will external contributors or security researchers interact with the repo? → Add **`CONTRIBUTING.md`** / **`SECURITY.md`**.
10. Is performance a stated requirement? → Add **`BENCHMARKS.md`**.

If in doubt, start with Tier 1 + `ARCHITECTURE.md` + `DECISIONS.md` and add others as the project grows and friction reveals which are needed.
