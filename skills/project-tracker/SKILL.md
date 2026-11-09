---
name: project-tracker
description: Keeps a project's state written down so the next developer or agent can pick it up cold - what was requested, what's in progress, what's done and verified, and where work stopped. Use at the start of work in a repo that has docs/HANDOFF.md, when the user asks for a feature, reports a bug or agrees to a refactor, after any verified change, and before stopping with work unfinished. Also use when asked to set up tracking, a dev log, a feature tracker, a work log or a handoff note.
---

# Project Tracker

Three files in the project's `docs/`:

| File | Holds | Edited how |
|---|---|---|
| `PROJECT-TRACKER.md` | Every item, with its permanent ID and current status | Rows added, then updated in place |
| `IMPLEMENTED.md` | One entry per verified completion, newest first | Append only |
| `HANDOFF.md` | Where things stand right now and what's next | Rewritten each time, under ~40 lines |

## IDs

An ID is permanent. Its prefix says what the item is, never how far along it is, so the ID never changes while the work moves from requested to done.

- `F-001` feature, or anything the user asks to be built or changed
- `B-001` bug
- `C-001` internal change: refactor, dependency bump, tooling, cleanup

Numbers count up per prefix and are never reused, including for dropped items.

## Statuses

`requested` → `in progress` → `done`, plus `blocked` (say on what) and `dropped` (say why).

`done` means verified: a command ran and passed, or the user confirmed it in the running app. Code that is written but unchecked stays `in progress` with "unverified" in the notes. Never mark an item done because the code was written.

## When to update

- **Session start.** If `docs/HANDOFF.md` exists, read it and the open rows of `PROJECT-TRACKER.md` before anything else.
- **New work.** When the user asks for a feature, reports a bug, or agrees to a refactor, add a row: `requested`, or `in progress` if you're starting now. Questions, explanations and one-line tweaks get no row.
- **Verified completion.** Move the row to Closed as `done`, and append an entry to `IMPLEMENTED.md`.
- **Stopping.** Before ending a session with work unfinished, or when the user says they're done for now, rewrite `HANDOFF.md`.

Update the tracker in the same change as the code, so it never lags behind the repo. Group small related edits under one item rather than one item per commit.

## Setting it up

If the repo has no `docs/PROJECT-TRACKER.md`, offer once to set it up the first time you make a meaningful change there. If the user declines, don't offer again that session. Don't offer outside a git repo or for throwaway scripts.

On setup:

1. Copy the three files from this skill's `templates/` into the project's `docs/`.
2. Seed the tracker with what's evident now: the current task and anything the user names as pending. Don't mine git history for a backlog.
3. Point other agents at it. Append this to `AGENTS.md` and to `CLAUDE.md` where they exist, or create `AGENTS.md` if neither does:

   ```markdown
   ## Project state
   Read docs/HANDOFF.md first, then the open items in docs/PROJECT-TRACKER.md.
   ```

## Writing entries

Follow the formats in the templates. Two rules carry most of the value:

- **Verification names what actually ran and what it returned**, such as "`npm test` - 42 passed" or "user confirmed the login flow in the browser". "Tests pass" with no command is not verification.
- **Handoff "Next" steps are concrete enough to start without asking**: a file, a function, a failing case. "Continue the auth work" is not a next step.

Keep entries short. Git history already holds the diff, so describe what now works differently, not every line that changed.

## What this doesn't replace

- **Git history** records each change line by line. Don't restate diffs.
- **`.claude/worklog.md`**, written by `/master`, records the decisions and rejected alternatives for one run. The tracker records items and their state. When a run wrote a worklog entry, link it from the `IMPLEMENTED.md` entry instead of copying it.
- **A user-facing CHANGELOG** is written for users. The tracker is written for whoever works on the project next.
