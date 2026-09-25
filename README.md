# vibe-check

> Vibe check for vibe coders who care about code quality.

An opinionated `AGENTS.md` template that tells a coding agent how to work in
your repo: keep changes small and code simple, follow the project's conventions,
and verify the result before calling it done.

## What it is

Left to their defaults, coding agents tend to invent their own conventions, add
more than was asked for, or report success before checking. This template lists
the conventions and workflow you'd otherwise keep repeating in prompts, so the
agent reads them at the start of every task.

It's one markdown file with nothing to install. The rules lean toward simplicity
and small diffs, which won't suit every project or team, so change whatever
doesn't fit.

## What's inside

| Section | What it covers |
|---|---|
| 1. Project | Stack, layout tree, do-not-touch paths, architecture, commands, configuration, setup & deploy steps |
| 2. Documentation | Where docs live, and keeping them updated alongside the code |
| 3. Coding conventions | Naming over commenting, small functions, boundary validation, testing |
| 4. Workflow | Think before coding, minimal diff, clean up, watch it actually work |
| 5. Notes | Project-specific gotchas, kept short |

## Usage

It works best on a scaffolded project — framework initialised, directory layout
in place, build and test commands working. The template is filled in from what's
in the repo, so on an empty folder the agent has little to go on and tends to
make things up.

1. Copy [AGENTS.md](AGENTS.md) into the root of the project.

2. Ask the agent to fill it in, for example:

   > Fill in every `<FILL-IN>` in AGENTS.md from this repo, as briefly as you
   > can while staying unambiguous. Ask me anything the code can't answer. Then
   > delete the setup block at the top.

   Review what it wrote. A wrong test command does more harm than an empty row.

3. Once filled in, the setup block is deleted and this line stays:

   > **Keep this file current, not busy.** It is meant to sit still. Edit it
   > only when a change to the repo invalidates something written here. Keep
   > edits short; this file is read in full on every task.

4. Tailor it. Add a section or a clarifying line when the project needs one, and
   delete sections that will never apply rather than marking them "not
   applicable". Record only what differs from defaults — anything the agent can
   read from config in seconds mostly just costs context.

## Agent compatibility

`AGENTS.md` in the repo root is read by many coding agents. If yours looks for a
different filename, symlink it rather than keeping two copies in sync:

```bash
ln -s AGENTS.md CLAUDE.md     # or .cursorrules, .github/copilot-instructions.md, ...
```

## Tips

- The file is read on every task, so every line costs context. Keep it short.
- Rules a linter, formatter or type-checker already enforces don't need to be in
  there — the tool catches them anyway.
- A rule still applies when the repo doesn't have the thing yet. No docs folder
  just means creating one when it's needed.
- Out-of-date instructions can mislead an agent more than missing ones. Fix them
  in the same change that makes them stale.
- Treat it as a reference, not a log. Progress notes and decision history belong
  in commit messages, or agents tend to keep appending to it.
