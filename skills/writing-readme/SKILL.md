---
name: writing-readme
description: Use when a project's plan has just been split into phases and confirmed, when a phased project has no README.md, when a plan task finishes in a phased project, or when your human partner asks to update the README ("README 업데이트해")
---

# Writing the README

The project plan is the document that lists the phases (the 기획서), not an implementation plan in `.superpowers/plans/`, which carries out one phase. A project whose project plan is split into phases, even into one, keeps a README.md with three sections, written in the project plan's language, status words included:

1. **Intro** under the project name: two or three sentences from the project plan on what the project does and for whom.
2. **How to run:** install steps, the run command, one example. If the program takes input, add what it needs, from the project plan and the code: the input file format (required columns or fields), and the names of required keys and environment variables, never their values. Where the plan and the code differ, follow the code. Leave this section out until runnable code exists.
3. **Phase status:** one line per phase in the project plan, `Phase <N>: <name> - not started | in progress | done (<YYYY-MM-DD>) | stopped (<YYYY-MM-DD>) - <deliverable>`. The deliverable is a one-line summary of what the phase delivers, from the project plan's phase content. Phases only; no task lines.

Put nothing else in a README you create. In a README that already exists, add or fix these three sections and leave the rest as your human partner wrote it. If the file map has no README.md line, add one.

## When

**Phases confirmed, or no README.md in a phased project:** create it with the intro and phase status. Add how to run only if runnable code exists already. Leave it uncommitted; superpowers:executing-plans commits it at setup.

**Phase starts:** mark that phase in progress.

**Task ends, before its last commit:** change the README only if one of these happened, and put the change in that commit:

- The task finished the phase: mark it done with today's date.
- The task changed how to run: the entry point, command options, the input it needs, or what has to be installed. A task that first makes the code runnable counts.

Neither happened: leave README.md untouched.

**Your human partner asks to update the README:** compare every section with the current state. Intro against the project plan. How to run against the entry point, the option parsing, the code that reads input and environment variables, and the dependency files. Phase status against the project plan and `git log`. Fix what differs and report what you changed.

Check commands by reading the code; do not run them to verify the README.
