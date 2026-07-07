# Score Claimer HTML

![License](https://img.shields.io/badge/license-MIT-green)
![Version](https://img.shields.io/badge/version-0.4.0-blue)
![Platform](https://img.shields.io/badge/platform-static%20HTML-orange)

[简体中文](README.zh-CN.md)

A single-file static HTML tool for logging in with an existing SMS flow and claiming available score missions from the browser.

> Unofficial third-party utility for personal study and automation experiments. It is not affiliated with, endorsed by, or certified by any upstream service provider.

## Why

The original app contains many unrelated features. This folder keeps only the score-claiming workflow so it can be published as a small GitHub Pages site instead of dragging the whole Flutter project around like a suitcase full of bricks.

## Core Features

- Phone, image captcha, SMS code login.
- Local `token`, `uid`, and `eid` persistence through `localStorage`.
- Copy, download, paste-import, and file-import login payload backups.
- Public-use risk notice and login consent gate.
- 60-second SMS request cooldown.
- Optional browser Persistent Storage request for longer local login retention.
- Fetch score balance and mission list.
- One-click serial claiming through `score-send`.
- Forced mission refresh and confirmation before one-click claiming.
- MD5 signing ported into plain browser JavaScript.
- Daily check-in support with server-side `limits` respected.
- H5 missions are hidden from the claim list.
- Each `refId` is attempted at most once per one-click claim run.
- `code == -98` retries up to three attempts for the current mission.

## Screenshots & Demo

This is a static page. Open `index.html` through an HTTP server or publish this folder with GitHub Pages.

## Quick Start

Local preview:

```bash
python -m http.server 5173
```

Then open:

```text
http://127.0.0.1:5173/
```

GitHub Pages:

1. Create a new GitHub repository.
2. Upload the contents of this folder.
3. Enable Pages from the repository settings.
4. Use the published URL to open `index.html`.

## Engineering Quality

- No package manager or build step required.
- No bundled secrets or account data.
- The page uses direct browser `fetch` calls to the upstream API.
- Claiming is intentionally serial and rate-limited by delay.

## Project Docs

- `index.html`: the complete static tool.
- `LICENSE`: MIT license inherited from the source project.
- `.nojekyll`: keeps GitHub Pages from applying Jekyll processing.

## Privacy & Security

This tool stores login data in browser `localStorage` in plain text. That is convenient, but not secure against someone who can access your browser profile. Do not publish real tokens, screenshots containing tokens, copied login payloads, or downloaded backup files.

Downloaded login backups are plain JSON files containing sensitive account tokens. Keep them only on private devices you control. Do not upload them to GitHub, cloud note apps, issue trackers, chats, or screenshots.

Login data is scoped to the same browser profile and the same deployed origin. Keeping one stable GitHub Pages domain helps the browser restore the local login state for a long time, especially when Persistent Storage is granted. It still cannot prevent manual site-data clearing, private browsing cleanup, browser changes, domain changes, or upstream token expiration.

SMS login is still manual. This project does not bypass captcha or SMS verification.

## Release & Updates

Current standalone publishing folder version: `0.4.0`.

`0.2.0` adds public-use safety copy, a consent gate, SMS cooldown, last refresh time, and a pre-claim confirmation flow.

`0.3.0` adds a browser Persistent Storage request and visible local-storage persistence status.

`0.4.0` adds downloaded login backups and JSON backup file import for easier long-term recovery after browser data loss.

## Roadmap

- Optional Cloudflare Worker runner for scheduled claiming.
- A small status export for the latest claim result.
- Better error messages for expired login sessions.

## Troubleshooting

- If the page cannot load missions, open it through `http://` or GitHub Pages instead of `file://`.
- If login state disappears, import a previously downloaded login backup or log in again with SMS.
- If claiming fails repeatedly, refresh missions first and check whether the upstream token has expired.

## Contributing

Keep the scope narrow. This is a score-claiming tool, not a rebuilt mobile app.

## License

MIT. See [LICENSE](LICENSE).
