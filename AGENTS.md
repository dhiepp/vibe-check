# AGENTS.md

**Setup — delete this block once you've done it.** This file ships as a template.

- Fill in every `<FILL-IN>` from what you find in the repo. Ask the user when the code can't answer it; don't guess.
- Otherwise leave the file intact. Don't reword, reorder or "improve" the rules as written — filling in the blanks is the job.
- Add anything project-specific a future agent would otherwise have to rediscover, as a new section or a clarifying line, and only where the project genuinely needs it.
- Record what **differs from defaults**. Skip whatever an agent can assume from the stack or read from config in seconds.
- **Be concise.** Write what you fill in or add at the shortest length that stays unambiguous: one rule per line, no preamble, no rationale a reader doesn't need, nothing another line already says.
- A rule still holds when the repo doesn't have the thing yet. No docs folder or no test runner doesn't void the guidance — it just means you create it, or use what's available, when the work calls for it.
- Delete any convention bullet this project's linter, formatter or type-checker already enforces. The tool states it better, and at the moment it matters.
- Delete a section only when its rule could never apply to this project. Never leave it in place with a note saying it's not applicable here.
- Then delete this block, leaving the line below in its place.

> **Keep this file current, not busy.** It is meant to sit still. Edit it only when a change to the repo invalidates something written here. Keep edits short; this file is read in full on every task.

---

## 1. Project

| Item | Value |
|---|---|
| Name | `<FILL-IN>` |
| Purpose | `<FILL-IN>` |
| Language(s) | `<FILL-IN>` |
| Framework(s) | `<FILL-IN>` |
| Runtime / toolchain | `<FILL-IN>` |
| Datastore | `<FILL-IN>` |
| Package manager | `<FILL-IN>` |

### Layout

`<FILL-IN: the organising principle — where source, tests, config and docs live, and how modules are grouped (by layer, by feature, by package). Enough to know where a new file belongs; not a full tree.>`

### Commands

| Task | Command |
|---|---|
| `<FILL-IN: one row per command this project actually has — install, run, build, test, lint, format, type-check, migrations, anything else needed daily>` | `<FILL-IN: the exact invocation, run from the repository root>` |

### Environment

Never commit a `.env`.

| Variable | Purpose / default |
|---|---|
| `<FILL-IN>` | `<FILL-IN>` |

### Build & deploy

`<FILL-IN: how this ships — build output, container/packaging, target platform.>`

---

## 2. Documentation

- Documentation goes wherever this project already keeps it; if there's no convention yet, use `/docs`. No planning, analysis or summary documents unless asked.
- Read the relevant docs before touching unfamiliar code, and update them in the same change when behaviour, architecture or commands change. Stale docs are worse than none.

`<FILL-IN: docs an agent must read before working here>`

---

## 3. Coding conventions

### Naming over commenting

- Names must make the code self-explanatory. If you want to comment *what* something does, rename it instead.
- One job per function, and the name says which. Booleans read as predicates. Abbreviate only where the language or this repo already does.
- Comment only when the *why* is non-obvious: a hidden constraint or invariant, a workaround for a specific bug, behaviour that would surprise a reader, the source of a non-trivial formula.
- Never restate the code, and never reference the current task, ticket or caller — that belongs in the commit message and rots.

### Structure

- Small functions and files, split along responsibility lines. Early returns over nesting. No magic numbers or strings.
- Validate at system boundaries (user input, external APIs, files) and treat what crosses them as hostile: parameterised queries, escaped output, validated schemas, least privilege.
- No dead code, unused imports, or unattributed TODOs.

### Dependencies and scaffolding

- Add a dependency only when nothing already in the repo or the standard library does the job. Say why in the commit.
- Anything the toolchain can generate — UI components, migrations, boilerplate — is created with the official command, never hand-written or copied in.
- Never hand-edit generated files. Change the source and regenerate.

`<FILL-IN: the generator commands, and which paths are generated>`

### Verification

- Every behaviour change ships with proof it works — a test where the repo has a framework, otherwise the thing run and observed.
- Where tests exist: reproduce a bug with a failing test before fixing it, names describe behaviour, one concern each, no logic in tests.
- Never weaken or delete a test to make it pass. If a test is wrong, say so.

---

## 4. Architecture

`<FILL-IN: this project's actual architecture — the layers or modules, what each owns, which way dependencies are allowed to run, and the boundaries that must not be crossed. Note caching, encryption and other behaviour invisible from a file listing. Link to the architecture doc if substantial.>`

- Consistency over local optimality: follow established patterns, raising one that seems wrong rather than silently diverging.
- Secrets come from the environment, never source. Config that genuinely never varies can be a constant; anything that differs per environment cannot.

---

## 5. Workflow

### Think before coding

1. **Understand the goal.** State what "done" means in one checkable sentence before touching anything — not "add validation" but "invalid input is rejected, and I can point at the test or the run that shows it".
2. **Don't hide confusion.** Where ambiguity would change the design, stop and put the plausible readings to the user rather than silently picking one. Otherwise choose sensibly and say what you assumed.
3. **Read first.** Explore the relevant code, tests and docs. Never guess at an API you could look up.
4. **Plan.** Outline the steps and affected files before writing, each paired with how you'll verify it. For large or risky changes, share the plan and wait for agreement.

### Simplicity first and foremost

- The simplest thing that fully solves the problem wins; boring and explicit beats clever and compact. If a simpler approach than the one requested exists, say so before building.
- No speculative abstraction — wait for the third concrete use. Three similar lines beat a premature helper.
- If a change grows beyond what was asked, stop and split it. If it came out several times longer than it needed to be, rewrite it — assume a senior reviewer will call it overcomplicated.

### Change only what you must

- Minimal diff: edit rather than rewrite. No drive-by refactors, reformatting, or features, flags, compatibility shims and error handling beyond scope — mention what you spot, don't fix it uninvited.
- Clean up what *your* change created or orphaned: temp files, scratch scripts, debug logging, experiment code, now-unused imports, variables and functions. Leave pre-existing dead code alone unless asked.
- Review the diff before finishing. If you broke something along the way, fix it.

### Watch it work

- Done means every check the repo has passes with zero new warnings *and* you watched the behaviour work. No test framework means verification is manual (run the app, call the endpoint, execute the command), not skipped.
- If you can't verify in this environment, say so plainly. Never claim a success you didn't observe.
- When something fails, find the root cause. Don't retry blindly or bypass checks (`--no-verify`, skipped tests).

### Version control

- Small atomic commits explaining *why*. Follow the repo's existing message style (`<FILL-IN>`).
- Don't commit unless asked. Never push, force-push, rebase shared branches or delete branches without explicit instruction.

### Blast radius

- Local reversible work — editing, testing, reading logs — proceeds freely.
- Confirm first for anything destructive, hard to reverse, or visible to others: deleting files or branches, dropping data, migrations against shared databases, sending messages, opening or closing PRs, touching CI/CD or permissions, adding or removing dependencies.
- Unexpected files or branches may be work in progress. Investigate before removing, and prefer moving aside to deleting.

### Communication

- Be brief: what you did, what's next.
- Name the blocker when blocked.
- Disagree with a reason, then follow the decision.

---

## 6. Notes

`<FILL-IN: at most five lines. Each names a concrete file, command or error, and each is something an agent would otherwise get wrong or have to ask about. Nothing inferable from the config, nothing already covered above, nothing you haven't actually hit. Finding none is the normal outcome — then delete this line and leave the section empty.>`

Add a line later only when you had to stop and ask the user something the code couldn't answer. Keep only what an agent must see unprompted, and move the rest into the docs as it gets crowded.
