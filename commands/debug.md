---
description: Find the root cause of a bug by reproducing and narrowing it, not by guessing at fixes
argument-hint: <the symptom — what you saw, and what you expected>
---

You are debugging. The goal is the **cause**, not a change that makes the symptom go away. Those are different outcomes and only one of them holds.

**Symptom:** $ARGUMENTS

## Method

1. **Reproduce it before theorising.** A bug you cannot trigger on demand is a bug you cannot claim to have fixed. Get to a command, input, or sequence that fails every time. If it fails only sometimes, that is information — record the rate and look for shared state, ordering, time, or concurrency before anything else.

   If you genuinely cannot reproduce it, say so and stop guessing. Ask for the version, the exact input, the full error, the environment. A fix shipped against an unreproduced bug is a coin flip.

2. **Read the actual error.** All of it, including the parts that look like boilerplate. The frame that matters is often not the top one. Note the real values in the message — a path, an index, a type — and check them against what you assumed they were.

3. **Narrow before you explain.** Guessing at causes scales badly; halving the search space does not. Narrow along whichever axis is cheapest:
   - **Time** — `git bisect` between a known-good and known-bad commit. Automate it with `git bisect run <cmd>` when the check is scriptable.
   - **Input** — shrink the failing case until removing anything else makes it pass. A one-line repro usually names its own cause.
   - **Code path** — confirm at the midpoint whether state is already wrong. Then recurse on the half that contains the transition from right to wrong.

4. **Form a hypothesis that predicts something you have not looked at yet.** "It's a null" is not a hypothesis; "`user.profile` is null for accounts created before the migration, so line 88 throws for exactly those rows" predicts a query you can run. Run it. A hypothesis that explains only what you already saw cannot be wrong, which makes it useless.

5. **Find where the invariant first breaks.** Follow the bad value upstream to the point where correct becomes incorrect. The crash site is usually the victim, not the culprit — fixing there is how you get a null check that hides a corrupt record for another six months.

6. **Prove the fix.** Write the test that fails on the current code and passes after. Run it both ways and report both. Then run the whole suite — a fix that breaks two other things is not a fix.

## Rules

- **Change one thing at a time.** Multiple simultaneous changes mean you learn nothing from the result and cannot revert cleanly.
- **Never suppress the symptom** — no swallowed exception, no retry loop, no defensive check at the crash site — unless you can state why the underlying condition is legitimate and expected.
- **Say when you are unsure.** "This fixes it and I know why" and "this makes it stop and I don't know why" are different reports. The second is still worth delivering, but it must be labelled, because it will come back.
- If the root cause is out of scope to fix properly, say what the proper fix is and what the stopgap costs. Do not quietly ship the stopgap as if it were the fix.

## Output format

**Symptom** — what fails, and the exact command or input that triggers it.

**Root cause** — the mechanism, at `path:line`. Why this produces that symptom, in the causal order it happens.

**Evidence** — what you ran and what it showed. The bisect result, the narrowed input, the value you printed. Not "I verified" — the output.

**Fix** — the change, and why it belongs at this level rather than at the crash site.

**Proof** — the test, failing before and passing after, with both runs shown.

**Related** — other places the same mistake appears. Grep for the pattern; a bug of this shape is rarely alone.
