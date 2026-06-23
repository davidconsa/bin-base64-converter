# Project: bin-base64-converter

> Browser-based binary ↔ Base64 converter. 100% client-side, multi-file, ZIP batch export.

## Stack

- **Language**: Vanilla JavaScript (ES6+), HTML5, CSS3
- **Runtime**: Browser only — no Node.js, no build step
- **Dependencies**: JSZip 3.10 (CDN via Cloudflare)
- **Font**: Inter (Google Fonts)
- **Other**: FileReader API, Blob/URL.createObjectURL, Clipboard API

## Project structure

```
.
├── index.html        # Single-page app: HTML + embedded CSS (~100 lines) + inline JS (~300 lines)
├── README.md         # Project description (minimal)
├── AGENTS.md         # This file — AI-assisted development guide
├── .vscode/
│   └── settings.json # VS Code config (Snyk org)
└── .atl/             # Skill registry for AI tooling (auto-generated)
    ├── skill-registry.md
    └── .skill-registry.cache.json
```

> **Note:** No other source files, build scripts, test files, or configuration files found. The entire application lives in `index.html`.

## Architecture rules

### Single-file application
- All HTML, CSS, and JS coexist in `index.html`. CSS is in a `<style>` block, JS is in a single `<script>` block at the bottom.
- No module system, no bundler, no build step — the file is served as-is.

### State management
- Application state lives in global arrays: `encFiles`, `decFiles`, `hist`.
- Each state array is mutated directly (push/splice). Corresponding render functions update the DOM.

### UI conventions
- **CSS**: Custom properties on `:root` for colors, spacing, radii, shadows. BEM-like naming (`.fl-head`, `.fl-body`, `.seg-btn`, `.frow-name`).
- **Spanish UI**: All labels, placeholders, status messages, and tooltips are in Spanish.
- **Events**: Mix of `onclick` attributes in HTML and `addEventListener` in JS for drag-and-drop.
- **Feedback**: Status banner (`sbanner`) with three variants: `success`, `error`, `info`. Hidden via `.show` class toggle.

### Conversion modes
- **Encode** → Binary file(s) to Base64 string(s), exported as `.base64.txt` files inside a ZIP.
- **Decode** → Base64 string (textarea or `.txt`/`.b64` file) to binary `.bin` file(s), exported as ZIP for multi-file.

### Key functions
- `toBuf64(buf)` → chunked buffer-to-Base64 conversion (8KB chunks avoids stack limits)
- `isB64(s)` → validates Base64 format (regex + length mod 4)
- `triggerDownload(blob, filename)` → creates temporary anchor element and clicks it
- `fmt(n)` → human-readable file sizes (B/KB/MB/GB)

## Dev commands

No build system, package manager, or test framework is configured. The project is a static HTML file.

| Command                     | What it does                                    |
|-----------------------------|-------------------------------------------------|
| `open index.html`           | Open the app in a browser (no server needed)    |
| `python3 -m http.server`    | Serve locally (optional — needed for JSZip CDN) |

**No test framework, no linter, no TypeScript compiler is configured.** The project has no `package.json`, `tsconfig.json`, or `jest.config.*`.

## Skills

Project-specific skills are not applicable — the project is a single vanilla HTML/CSS/JS file with no backend, no TypeScript, no testing framework, and no build tooling.

The following general-purpose skills are available via the skill registry (see `.atl/skill-registry.md` for the full list):

| Skill              | When to use                                                    |
|--------------------|----------------------------------------------------------------|
| `commit-gen`       | Generating git commit messages                                 |
| `branch-pr`        | Creating pull requests                                         |
| `work-unit-commits`| Organizing commits as reviewable units                         |
| `tech-research`    | Researching libraries, APIs, or approaches                     |
| `comment-writer`   | Writing review or collaboration comments                       |
| `issue-creation`   | Creating GitHub issues                                         |
| `cognitive-doc-design` | Writing guides, READMEs, or architecture docs             |
| `skill-creator`    | Creating new AI-development skills                             |
| `judgment-day`     | Running adversarial code review                                |

**Skills with TypeScript/AWS/Build dependencies listed in the registry (e.g., `typescript`, `jest`, `inversify`, `fetch`, `middy`, `terraform`, `nestjs`, `async-concurrency`, `serverless-local`, `zod-4`, `io-*`, `architech-bcp`) do not apply to this project.**

## Conventions

- **Spanish UI**: All user-facing text in Spanish (`es` locale in `<html>`, labels, placeholders, error messages).
- **camelCase functions**: `handleFiles`, `renderEncList`, `triggerDownload`, `decodeAction`.
- **File naming**: Encoded output → `{original}.base64.txt`. Decoded output → `{original}.bin` (after stripping `.base64.txt`, `.b64`, `.txt`).
- **Single-file pattern**: Everything in `index.html` — no external CSS or JS files beyond CDN dependencies.
- **Progressive enhancement**: All state reflected in DOM immediately; no framework reactivity.
- **No external backend**: 100% client-side processing — the badge reads "100% local · Sin servidores".
