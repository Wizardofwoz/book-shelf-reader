# Book Shelf Reader

Built by **Chandra** at Walk & Hack, the AI Tinkerers NYC × Twilio build-while-you-walk event in Central Park on October 24, 2026. The app was built by texting a coding agent from the park; this repo is the code that came out, packaged so it runs on your own machine.

Little Library: a book reader in one HTML file. Five public-domain stories (Wilde's Happy Prince tales, Poe's Masque of the Red Death) are embedded, you can add your own books, and the reader paginates with CSS columns so changing the font size reflows the pages and keeps your place. Books sit on wooden planks; delete, mark as read, restore. Two earlier builds from the same walk are kept alongside: `squirrel.html` (whack-a-mole) and `planets.html` (a solar system game).

## Run it

```bash
pnpm install
pnpm dev
```

Open http://localhost:3000, or just open any of the three HTML files in a browser; each is self-contained with no libraries or external assets.

## Layout

- `index.html` the reader (the book texts are inlined as JSON in a script block).
- `squirrel.html`, `planets.html` the earlier games.
- `src/` an unused React scaffold; `vite.config.ts` dev server config.
- `NOTES.md` the builder's working notes from the event, kept as-is.
