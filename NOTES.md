# BRAIN

## What this is
Sandbox app serving single-file HTML apps from the repo root via Vite (port 3000).

## Current state
- `index.html` = Little Library book reader (5 public-domain stories embedded as JSON) + user-added books (localStorage `reader:custom`), Delete on every book (built-ins tracked in `reader:deleted`, "Restore" button brings them back), Mark-as-read toggle (`reader:read`), search box, sort select (`reader:sort`: shelf/title/author/status).
- `squirrel.html` (whack-a-mole) and `planets.html` (solar system game) are earlier tasks, kept as separate pages.
- Each page is fully self-contained (no libs, no external assets). `src/` (React) is unused/not loaded.

## Stack & key choices
- Vanilla HTML/CSS/JS. Reader paginates with CSS multi-columns on `#flow` + translateX (page = column), so font-size changes re-flow; position stored as fraction `f` in localStorage `reader:pos:<id>` so it survives font/resize changes.
- Book texts: Project Gutenberg #902 (Wilde, Happy Prince and Other Tales) and #1064 (Poe, Masque of the Red Death). Preprocessed offline (strip header/picture tags, join lines to paragraphs), inlined in `<script type="application/json" id="booksData">`.

## Decisions
- UI pass: books sit on wooden planks, 56px+ Delete/Mark-as-read buttons, sticky bottom "Add book", typed toasts (ok/del), focus returns to opener/new book/next book, modal Tab trap, empty states (no matches / empty shelf).
- index.html is GENERATED: edit /tmp/opencode/build/template.html then `node build.mjs` (injects books.json). If /tmp was wiped, edit index.html directly (booksData JSON block is large).
- Each new task replaced index.html; prior game was copied to its own file first so nothing is lost.

## Gotchas & environment facts
- No browser can run: playwright chromium downloads but lacks libglib/nss etc., no root/apt. Verify logic with jsdom (npm i jsdom in /tmp/opencode/pw, stub getBoundingClientRect/scrollWidth). Real CSS-column pagination is therefore not visually verified.
- Check page serves: `curl -s http://127.0.0.1:3000/ | grep -c "Little Library"`
- Untracked `dist/` in repo root is not ours (platform build output).

- Agent-side "Provider rejected the request" build error is NOT from the app: the app has zero fetch/API/key usage (`grep -nEi "fetch\(|api.?key" index.html`). Provider URL/model/key live in platform Settings, not editable from the sandbox.
