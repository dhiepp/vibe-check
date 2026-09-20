# vibe-check

> Vibe check for vibe coders who care about code quality.

A single-file `AGENTS.md` template: the house rules you hand your coding agent
so that what it ships still passes a senior review.

## What it is

Coding agents are fast and agreeable. Left without instructions they invent
conventions, bolt on error handling nobody asked for, write four files where one
would do, and report success they never observed. `vibe-check` is the antidote —
one file, read in full on every task, that tells the agent how *this* repo works
and what "done" actually means.

It is a **template**, not a framework. Nothing to install, no dependency, no
runtime. You copy one markdown file into your project and fill in the blanks.

## What's inside

| Section | What it pins down |
|---|---|
| 1. Project | Stack, layout, the exact commands for build/test/lint, env vars, deploy |
| 2. Documentation | Where docs live, and the rule to update them in the same change |
| 3. Coding conventions | Naming over commenting, small functions, boundary validation, no dead code |
| 4. Architecture | Your layers and the boundaries that must not be crossed |
| 5. Workflow | Think before coding, minimal diff, clean up, verify until it actually works |
| 6. Definition of done | A checklist the agent has to answer to |
| 7. Project notes | Gotchas, generated files, forbidden areas |

The bias throughout: **simplicity first, minimal diff, no unverified success
claims.**

## Use it

1. Copy [AGENTS.md](AGENTS.md) into the root of your project.

2. Fill it in. Easiest path is to let the agent do it — open the repo and ask:

   > Fill in every `<FILL-IN>` in AGENTS.md from this repo. Ask me anything the
   > code can't answer. Then delete the setup block at the top.

   Do not let it guess. A wrong test command is worse than an empty row.

3. Delete the setup block once done, and keep the line below it:

   > **Keep this file current.** When the repo changes and something here goes
   > stale, fix it in the same change.

4. Trim what will never apply, and add what is specific to your project. Record
   what **differs from defaults** — anything the agent can read from your config
   in seconds is noise that costs you context on every task.

## Agent compatibility

`AGENTS.md` in the repo root is the cross-tool convention, picked up by most
current coding agents. If yours reads a different filename, point it at this one
rather than keeping two copies that drift:

```bash
ln -s AGENTS.md CLAUDE.md     # or .cursorrules, .github/copilot-instructions.md, ...
```

## Keeping it honest

- One file, read on every task — every line you add is paid for in context.
  Short beats thorough.
- A rule still holds when the repo doesn't have the thing yet. No `/doc` folder
  means you create one when the work calls for it, not that the rule is void.
- Stale instructions are worse than none. If a command in there no longer runs,
  fix it in the same change that broke it.
