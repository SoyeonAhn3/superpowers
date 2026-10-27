---
name: finishing-a-development-branch
description: Use when implementation is complete, all tests pass, and you need to decide how to integrate the work
---

# Finishing a Development Branch

## Overview

**Core principle:** Verify tests → Clean up plan files → Present options → Execute choice.

In this setup Git worktrees are not used. You integrate locally. Push or open a pull request only when your human partner asks for it; each push goes through an approval prompt. Never force-push.

**Announce at start:** "I'm using the finishing-a-development-branch skill to complete this work."

## Step 1: Verify Tests

Run the project's full test suite (`npm test` / `cargo test` / `pytest` / `go test ./...`).

**If tests fail**, report the failures and stop — the menu comes after a green suite:

```
Tests failing (<N> failures). Must fix before completing:

[Show failures]
```

**If tests pass:** continue to Step 2.

## Step 2: Clean Up Plan Files

The design doc (`.superpowers/specs/`) and plan (`.superpowers/plans/`) for this work were git-ignored scratch. Before deleting them, carry over what should outlive them:

- Why the work was built this way goes in the final commit message body.
- A placement rule worth keeping (e.g. "all date helpers live in `utils/date.py`") goes into the file map, under "여기에 두는 것" in the right CLAUDE.md.

Then delete this work's design doc and plan. Leave other plans' files alone; they belong to unfinished work.

## Step 3: Determine Base Branch

The base branch is whatever this work forked from — usually named in the
plan, the conversation, or the branch's upstream. If it is not already
known, ask: "This branch split from <your best guess> - is that correct?"
Confirm before merging: merging into the wrong base is expensive to undo.

If the work was done directly on the base branch with your human partner's consent, skip Steps 3–5: report the commits and stop.

## Step 4: Present Options

Present exactly these 2 options:

```
Implementation complete. What would you like to do?

1. Merge back to <base-branch> locally
2. Keep the branch as-is (I'll handle it later)

To push, ask me.

Which option?
```

Discarding the work happens only in response to your human partner explicitly asking for it (see below). Wait for their answer; the integration decision is theirs.

## Step 5: Execute Choice

### Option 1: Merge Locally

```bash
git checkout <base-branch>
git merge <feature-branch>
<test command>
```

If tests fail on the merged result: stop, leave the branch in place, and investigate — the merge is local and recoverable.

Once the merged result is green, delete the branch:

```bash
git branch -d <feature-branch>
```

### Option 2: Keep As-Is

Report: "Keeping branch <name>."

### If your human partner asks to discard the work

This path exists only as a response to an explicit request to throw the work away. Confirm first:

```
This will permanently delete:
- Branch <name>
- All commits: <commit-list>

Type 'discard' to confirm.
```

Wait for that exact confirmation. When it arrives, switch to the base branch and force-delete the branch:

```bash
git checkout <base-branch>
git branch -D <feature-branch>
```

## Common Rationalizations

| Excuse | Reality |
|--------|---------|
| "Tests passed earlier this session" | Run the suite on the tree you are about to integrate. A green run only proves the tree it ran on. |
| "They obviously want it merged" | Integration is your human partner's decision. Present the menu and wait. |
| "I'll push so it's backed up" | Push only when your human partner asks. Report and stop. |
| "The plan file might be useful later" | Code, tests, commit messages, and the file map are the record. A stale plan misleads the next session. |
| "They seem done with this feature — I'll offer to discard it" | The menu is complete as written. Discard happens only when your human partner asks for it in so many words. |
| "'Yeah, get rid of it' counts as confirmation" | Only the typed word `discard` authorizes deletion. |
| "The merged-result failure is probably flaky" | A failing merged result stops everything. The branch stays put while you investigate. |
| "The base branch is obviously main" | Confirm the fork point or ask. Merging into the wrong base is expensive to undo. |
