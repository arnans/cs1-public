# cs1-public

Public resources for the CS1 textbook — a 4-chapter computer science course for middle school students using the [GoGo Board](https://www.gogoboard.org).

## What's in this repo

This repo hosts reference pages and video tutorials that students access via QR codes and short links printed in the textbook. Content is served through **GitHub Pages** at:

**https://arnans.github.io/cs1-public/**

### Pages

| Page | Description |
|------|-------------|
| `ch01-robot-setup` | Video tutorial: setting up the robot car |
| `input-howto` | Video tutorial: using the GoGo Board's input ports |
| `output-howto` | Video tutorial: using the GoGo Board's output ports |
| `isensor-howto` | Video tutorial: using the integrated sensors |
| `codegogo-howto` | Video tutorial: connecting to code.gogoboard.org |
| `code-download-run-howto` | Video tutorial: downloading and running code |
| `touch-extension-howto` | Video tutorial: adding the GoGo Touch extension |
| `ch02-game-list` | Reference table of games for controller activities |

## How shortlinks work

The textbook uses **d.gogoboard.org** as a short URL domain. QR codes in the printed workbooks point to addresses like `d.gogoboard.org/input-howto`, which redirect to the corresponding GitHub Pages URL.

```
Student scans QR code
    → d.gogoboard.org/input-howto                (shortlink)
    → arnans.github.io/cs1-public/input-howto    (this repo, via GitHub Pages)
```

Redirects are managed in a separate repo ([url-redirect](https://github.com/arnans/url-redirect)) hosted on Cloudflare Pages.

## Adding a new page

1. Create a markdown file in this repo with Jekyll front matter:
   ```markdown
   ---
   title: Page Title
   ---

   Your content here (HTML like iframes is supported).
   ```
2. Commit and push — GitHub Pages will publish it automatically.
3. Add a redirect in the [url-redirect](https://github.com/arnans/url-redirect) repo's `_redirects` file pointing to the new page.
4. Generate a QR code for `d.gogoboard.org/SHORTNAME` and place it in the textbook.
