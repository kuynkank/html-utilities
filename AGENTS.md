# AGENTS.md

Guidance for AI agents building or editing tools in this repo.

## What this is

A collection of single-file HTML tools.


## Technical rules

Every tool must be:

- **One `.html` file** in the repo root, named in kebab-case (`screenshot-annotator.html`), with CSS and JS inline.
- **No React, no build step.** Plain HTML, CSS, and vanilla JS.
- **CDN-only dependencies**, from cdnjs or jsDelivr, and only when a well-known library clearly saves work (e.g. JSZip for ZIP export).
- **Small** — a few hundred lines, so any agent can read the whole file at once.
- **Client-side only.** Files are read with `<input type="file">`, drag-and-drop, or paste; nothing is uploaded. Outputs are generated in the browser and downloaded.

Also include:

- A `<title>` and `<meta name="description">`.
- Icons as inline SVG (Lucide style: 24×24 viewBox, `stroke="currentColor"`, stroke-width 2), not an icon font or CDN.
- A "Copy to clipboard" action wherever the tool produces text.
- Session state in `localStorage` under a namespaced, versioned key (`tool-name.session.v1`), wrapped in `try/catch`. Use URL params instead when the state should be shareable.
- `@media` rules so the layout works at narrow widths.

## Design language

Quiet and functional: the tool should look like a utility, not a landing page.

- **Background** `#fefefe`.
- **Font** `"Helvetica Neue", Helvetica, Arial, sans-serif` everywhere, including buttons, inputs, and canvas text.
- **Color only for content, not controls.** Controls are black, white, and grays; color is for the user's data (categories, highlights, charts).
- **Only what the task needs.** Every control should earn its place; no decorative gradients, illustrations, emoji, or glow effects.
- **Plain, short copy.** Labels say what things do. No taglines or marketing voice.
- **Space over boxes.** Group with whitespace before adding borders, dividers, or cards.
- **Subtle motion.** Quick hover and press feedback only; nothing that animates on its own.

## Adding a tool

1. Create `tool-name.html` in the root following the rules above.
2. Add a row to the Tools table in `README.md` (keep it alphabetical) with a one-line description.
3. Keep the README short — the tool should explain itself.
4. Test in a browser at desktop and narrow widths, and check the console for errors.

## Background

Adapted from Philip Levy's [web-tools AGENTS.md](https://github.com/pglevy/web-tools/blob/main/AGENTS.md), which draws on Simon Willison's [Useful patterns for building HTML tools](https://simonwillison.net/2025/Dec/10/html-tools/). Patterns from that article worth reaching for:

- **Copy and paste** as the main input/output — accept pasted content, transform it, copy it back out.
- **State in the URL** for anything worth bookmarking or sharing.
- **`localStorage`** for larger state and API keys (never commit keys).
- **CORS-enabled APIs** (GitHub, PyPI, Bluesky, LLM APIs) can be called directly from the page.
- **Generate files in the browser** — PNG via canvas, ZIP, PDF, ICS.
- **Pyodide / WebAssembly** when a task needs Python or a compiled library.
- **Remix existing tools** — point the agent at a similar tool in this repo as a starting template.
