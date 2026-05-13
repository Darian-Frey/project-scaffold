<!--
CLAUDE.skeleton.md — copy to CLAUDE.md and fill in placeholders.
See: development_documentation.md §Per-Document Specifications → CLAUDE.md
Handoff document for AI-assisted development sessions.
Always describes CURRENT state, not history (use CHANGELOG.md for history).
Refresh at the end of every significant session.
-->

# CLAUDE.md

## Project

{2–3 sentences. What this project is, what stage it's in.}

## Current state

What works, what's stubbed, what's broken. Be file-level specific.

- `src/{module}`: {status}
- `tests/{module}`: {status}
- `docs/`: {status}

## Active task

{The immediate next work item. Reference feature IDs from FEATURES.md (or claim IDs from CLAIMS.md for research). State acceptance criteria.}

**Acceptance:**
- {measurable condition}

## Architectural invariants

Rules that must not be violated. May reference DECISIONS.md or ARCHITECTURE.md for the full rationale.

- {rule that must hold}
- {rule that must hold}

## Build & test commands

```bash
{build command}
{test command}
{any other commands used routinely}
```

## Conventions

- {naming convention}
- {formatting / style}
- {commit message format}
- {comment style if non-obvious}

## Pitfalls

- See [ATTACK_VECTORS.md](ATTACK_VECTORS.md) for the canonical list of failure modes.
- {session-specific gotcha not yet promoted to a formal AV entry}

## Out of scope

Things the AI should not change without asking:

- {area or file}
- {area or file}
