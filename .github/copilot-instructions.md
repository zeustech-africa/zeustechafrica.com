## Purpose

This repository is a minimal, static single-page site. The goal of these instructions is to give an AI coding agent immediate, repository-specific context so it can make safe, correct edits without guessing project workflows.

## Big picture

- Single static HTML page at `index.html`. No build system, no package manager, and no server-side code.
- Assets (images) live alongside `index.html` (example: `zeustech-website copy.jpg`).
- Styling is in an inline `<style>` block inside `index.html`; there is no separate CSS file.

Why this matters: keep changes simple. Editing `index.html` is the primary change surface. Avoid introducing unnecessary tooling (bundlers, frameworks) unless the user asks.

## Key files to inspect

- `index.html` — the only source file. Examples to reference when generating changes:
  - The logo is referenced as `zeustech-website copy.jpg` via an `<img src="...">` tag.
  - CSS is inline in a `<style>` tag in the `<head>`.

## Project-specific conventions and patterns

- Filenames may include spaces (see `zeustech-website copy.jpg`). Prefer suggesting safer, space-free filenames in fixes (e.g., `zeustech-website.jpg`) and update the `src` in `index.html` when renaming.
- Keep styles in the head's `<style>` block unless the user requests extracting a separate `.css` file.
- Use semantic, minimal HTML edits: prefer changing text, attributes, or adding small structural elements rather than large rewrites.

## Workflows — how to build, test and serve locally

There is no build. To preview locally, run a simple static server from repository root. Example (suggested to user in PR notes):

```bash
# from repository root
python3 -m http.server 8000
# then open http://127.0.0.1:8000/
```

Or with Node (if Node is installed):

```bash
npx http-server -c-1 .
```

## Editing guidelines for AI agents

- Make minimal, atomic changes and include a short PR description summarizing the edit and why it was needed.
- If changing image filenames, update `index.html` references and mention the rename in the commit message.
- Preserve existing inline CSS unless extracting is explicitly requested. If extracting, create `styles.css` at repo root and update `index.html` to link it.
- Avoid adding build tooling. If the user asks for a build setup, propose a minimal plan and wait for confirmation.

## Example tasks and how to approach them

- Change the hero heading text: edit the `<h1>` inner text in `index.html` and preview via `python3 -m http.server`.
- Replace the logo with an optimized file: add the new image to the repo (no spaces in the filename), update the `src` attribute, and mention the filename change in the commit message.
- Convert inline styles to a stylesheet (only when requested):
  1. Create `styles.css` with the CSS from `<style>`.
  2. Remove the `<style>` block and add `<link rel="stylesheet" href="styles.css">` in `<head>`.

## What not to do

- Do not introduce new frameworks, build steps, or package managers without explicit user consent.
- Do not assume any CI, linting, or test suites exist — none are present in the repo.

## Where to ask for clarification

- For design or content decisions (copy, images), ask the user before changing.
- For introducing new tooling or restructuring the repo, present a short proposal first (1–3 steps) and wait for approval.

---

If any section needs more detail or you'd like rules for a proposed change (e.g., add CI, split CSS), tell me which approach you prefer and I will update this file.
