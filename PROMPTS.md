# Prompts

Starter prompts for opening a chat session against this standard. These are bootstrapping aids — once a project has a `CLAUDE.md`, the normal flow applies (Claude reads `CLAUDE.md` first, then other docs as needed for the active task).

Use these when **no `CLAUDE.md` exists yet**: a brand-new project, an existing repo that hasn't adopted the standard, or a Dormant project being revived from a state where the existing `CLAUDE.md` is stale.

Each prompt assumes you have either attached or made available [`development_documentation.md`](development_documentation.md). Adjust paths and project names to your situation.

---

## 1. Bootstrap a new project

Use when starting a project from scratch.

> I'm starting a new project called **{Project Name}**. Briefly: {one-sentence description of what it is and who it's for}.
>
> Read the development documentation standard at `development_documentation.md`. Then walk me through creating the Tier 1 documents in the order given by the standard's **Creation Order** section. For each document, ask me the questions you need answered before drafting it — don't guess at scope, priorities, or domain.
>
> Once Tier 1 is in place, use the **Quick Decision Guide** to recommend which Tier 2 and Tier 3 documents apply, and explain your reasoning for each.

---

## 2. Audit an existing repo against the standard

Use when adopting the standard for a project that already exists.

> I have an existing project that doesn't follow this standard. Read the development documentation standard at `development_documentation.md`, then review the project's current documentation: {list the relevant files or paths, e.g. `README.md`, `docs/`, any existing decision logs}.
>
> Identify the gaps between what exists and what the standard prescribes. Propose a minimal migration plan that leans on the friction test from the standard's **A note on cost** section — don't recommend adding documents that aren't currently causing real confusion. Order the proposed additions by leverage: highest value to add first, lowest value last.
>
> Flag anything in the existing documentation that conflicts with the standard (e.g. drifted status vocabulary, missing stable IDs, history mixed with current state) and propose how to reconcile.

---

## 3. Revive a Dormant project

Use when returning to a project after a significant gap.

> I'm returning to **{Project Name}** after roughly {N} months. Read the development documentation standard at `development_documentation.md`, then read the project's current `CLAUDE.md`, `README.md`, `DECISIONS.md`, and `ROADMAP.md`.
>
> Tell me:
>
> 1. What state the project appears to be in (status, last reviewed date, last completed work).
> 2. Which parts of `CLAUDE.md` are likely stale and need refreshing before I resume.
> 3. What the **Project lifecycle** section of the standard requires for the Dormant → Active transition.
> 4. Any decisions in `DECISIONS.md` whose reversal conditions may now be met given how much time has passed.
>
> Do not start work on the project itself yet — produce this status report first so I can review it before deciding what to resume.

---

## Notes on use

- These prompts deliberately keep Claude in a planning / questioning mode rather than letting it dive into output. The standard explicitly favours defining scope (FEATURES, CLAIMS) before writing implementation.
- If a prompt produces output that feels mechanical or wrong for your project, push back. The prompts are starting points, not contracts — your project's specifics should override them.
- Once any of these sessions produces a working `CLAUDE.md`, future sessions on the same project use the normal flow: Claude reads `CLAUDE.md` first, then proceeds.
