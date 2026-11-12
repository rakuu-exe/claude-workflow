---
name: code-style
description: House rules for writing code in this user's projects — simple, reusable, few comments, documented in docs instead. Use whenever writing or changing code, and when reviewing whether code is easy to read.
---

# Code style

The person who owns this code wants to open any file and understand it on the first read. Every rule below serves that.

## Simple first

- Write the plainest version that works. Add structure only when a second real use shows up.
- One function does one thing. If you need "and" to describe it, split it.
- Keep nesting shallow: return early instead of wrapping the rest of the function in an `if`.
- Name things for what they hold or do. A name that needs a comment is the wrong name.
- No abstraction for a single caller, no option nobody passes, no handling for a case that cannot happen.

## Reuse before adding

- Search for an existing component, hook, helper or token before writing a new one, and use it.
- When the same logic appears a second time, pull it into one place. Do not copy it a third time.
- Shared values (colours, spacing, durations, easings, breakpoints) live in one tokens file. Never repeat a raw value in a component.
- A reusable piece takes its data through arguments or props. It does not reach into the page around it.

## Comments

- Do not write a comment that repeats what the code says.
- Write one only for a reason the code cannot show: a workaround, a constraint from outside, a decision that looks wrong but is deliberate.
- Do not leave commented-out code or notes about what used to be there.

## Documentation instead

How things work is written down in the project, not scattered through the code:

- `README.md`: what the project is, how to run it, and a short "how it works".
- `docs/`: one page per part that needs explaining, written for someone opening the project cold.
- When you add or change something a reader would need explained, update the page that covers it in the same change. If no page covers it, add one.

## Before you call it done

- Read the diff once as someone who has never seen the project. Fix whatever made you stop.
- Remove anything you added that the task did not need.
