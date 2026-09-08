---
description: Start a new web project with the foundations already in place, so /launch-check finds nothing
argument-hint: <what you are building, and the stack if you have a preference>
---

You are setting up a new project. `/launch-check` audits for the foundations that never get done; you are the other half — you put them in at minute one, when each costs a line instead of a refactor.

**Project:** $ARGUMENTS

## Method

1. **Settle the stack before writing anything.** If the user named one, use it. If not, pick the boring default for what they described and say in one line why — do not present a menu. A static marketing page does not need a framework; a form that writes to a database does not need a SPA. Match the tool to the problem, and prefer what has the smallest number of moving parts that still does the job.

2. **Create the smallest thing that runs.** One page or one endpoint, actually working, verified by running it. Not a skeleton of empty folders — a project the user can start and see. Everything else is added onto something that already works.

3. **Put the foundations in as you go, not after.** Each of these is cheap now and expensive later:

   - **`.gitignore` first**, before the first commit — dependencies, build output, `.env`, editor state, OS files. A secret committed once is in the history forever, and the fix is rewriting history.
   - **Config through the environment.** A `.env.example` with every key listed and no real values; `.env` ignored. The app reads config in one place and fails loudly at startup if something required is missing — not on the first request in production.
   - **Error surfaces.** A 404 and a 500 page that look like the site. An error boundary if the framework has one. These are the pages users see on your worst day and the ones nobody remembers to make.
   - **The page shell.** `<title>`, meta description, Open Graph tags, viewport, `lang`, favicon. Semantic landmarks — `<main>`, `<nav>`, `<header>` — because retrofitting structure into a div tree is a rewrite, and screen readers depend on it.
   - **`robots.txt`.** Even if it only allows everything, its absence is a 404 in your logs forever.
   - **One example of each pattern the project will repeat** — one route, one component, one test, one migration if there is a database. The second of each gets copied from the first, so make the first one right.

4. **Verify it runs.** Start it. Load the page or hit the endpoint. Paste the output. A scaffold that has never been executed is a guess.

5. **Write the README last**, once you know what you actually built: what it is, how to run it, what environment variables it needs.

## Rules

- **Add a dependency only when the task at hand needs it.** Not because a project of this kind usually has one. Every package is a thing to update, audit, and eventually remove. If a dozen lines of standard library will do, write the dozen lines.
- **No placeholder code presented as finished.** A stub is labelled a stub, in the code and in your report.
- **Never generate legal text.** Create `/privacy` and `/terms` routes with a visible placeholder. A policy invented by an agent makes claims about data handling that nobody verified.
- **No analytics, no tracking, no consent banner by default.** Add them when the user asks, and then the consent mechanism has to actually gate the script rather than sit next to it.
- Do not build features that were not requested. The scaffold is the foundation, not the product.

## Output format

**Stack** — what you chose, in one line, with the reason.

**Created** — the tree, with a one-line purpose for each file you wrote. Skip generated lockfiles and vendor directories.

**Running it** — the exact commands, and the output proving you ran them.

**Foundations in place** — the checklist above, each marked done or deliberately skipped with the reason. This is what `/launch-check` will look for later.

**Next** — the two or three things to build first, given what they said they are making.
