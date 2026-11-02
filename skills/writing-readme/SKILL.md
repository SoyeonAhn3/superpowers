---
name: writing-readme
description: Use when a project's plan has just been split into phases and confirmed, when a phased project has no README.md, when a plan task finishes in a phased project, or when your human partner asks to update the README ("README 업데이트해")
---

# Writing the README

A project split into phases keeps a README.md with three sections, written in the plan document's language:

1. **Intro** under the project name: two or three sentences from the plan on what the project does and for whom.
2. **How to run:** install steps, the run command, one example. Until runnable code exists, one line saying it will be added after development.
3. **Phase status:** one line per phase in the plan, `Phase <N>: <name> - not started | in progress | done (<YYYY-MM-DD>)`. Phases only; no task lines.

Put nothing else in a README you create. In a README that already exists, add or fix these three sections and leave the rest as your human partner wrote it. If the file map has no README.md line, add one.

## When

**Phases confirmed, or no README.md in a phased project:** create it with the intro and phase status. Fill in how to run only if runnable code exists already.

**Phase starts:** mark that phase in progress.

**Task ends, before its last commit:** change the README only if one of these happened, and put the change in that commit:

- The task finished the phase: mark it done with today's date.
- The task changed how to run: the entry point, command options, or what has to be installed. A task that first makes the code runnable counts.

Neither happened: leave README.md untouched.

**Your human partner asks to update the README:** compare every section with the current state. Intro against the plan. How to run against the entry point, the option parsing and the dependency files. Phase status against the plan and `git log`. Fix what differs and report what you changed.

Check commands by reading the code; do not run them to verify the README.
