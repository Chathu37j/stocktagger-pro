# StockTagger Pro

A single-file, client-side AI metadata generator for stock photography, video, and audio/ringtone marketplaces. Upload media in bulk, generate SEO-friendly titles, descriptions, and keywords with AI, and export ready-to-upload CSVs for Adobe Stock, Shutterstock, Freepik, iStock, Pond5, and more.

No backend, no build step, no dependencies to install — it's one HTML file that runs entirely in your browser.

## Features

- **Bulk upload** — images, videos, and audio/ringtones, processed together
- **Multi-provider AI with auto-fallback** — add keys for Google Gemini, Anthropic Claude, OpenAI, and Groq; if one fails (rate limit, quota, outage) the app automatically retries with the next provider in your priority order
- **Real audio understanding** — Gemini and OpenAI (`gpt-4o-audio-preview`) can actually listen to audio clips, not just guess from the filename
- **Video frame extraction** — pulls a representative frame client-side (via `<canvas>`) to send for analysis
- **SVG support** — vector files are rasterized in-browser before being sent to any vision model
- **Per-field copy buttons** — copy title, description, or keywords individually
- **Multi-platform export** — Adobe Stock, Shutterstock, Freepik/POD, iStock/Getty, Pond5, plus Facebook caption and YouTube title/description/tags as plain text
- **Light/dark theme toggle**, grid/list view, drag-and-drop or tap-to-upload
- **Priority or balanced** provider strategy, with up/down reordering (works on both desktop drag and mobile tap)

## Getting started

### Option 1 — GitHub Pages (recommended)

1. Push this repo to GitHub.
2. Go to **Settings → Pages**, set the source to the `main` branch, root folder.
3. Your app will be live at `https://<your-username>.github.io/<repo-name>/`.

### Option 2 — Run locally

Just open `index.html` directly in a browser. No server, no build step required.

> **Note:** open it in a real browser tab (not an in-app file previewer / "Open with" viewer embedded in another app) — some of those sandboxes block outbound network requests, which will make every provider call fail with a generic network error.

## Setting up API keys

Click **Settings** in the app and add a key for any provider you want to use:

| Provider | Get a key | Supports |
|---|---|---|
| Google Gemini | [aistudio.google.com/apikey](https://aistudio.google.com/apikey) | Images, video frames, **real audio** |
| Anthropic Claude | [console.anthropic.com/settings/keys](https://console.anthropic.com/settings/keys) | Images, video frames |
| OpenAI | [platform.openai.com/api-keys](https://platform.openai.com/api-keys) | Images, video frames, **real audio** (wav/mp3 only) |
| Groq | [console.groq.com/keys](https://console.groq.com/keys) | Images, video frames (fast, generous free tier) |

You can add just one, or all four for automatic fallback. Reorder priority by tapping the up/down arrows next to each provider in Settings.

**Your keys never leave your browser.** They're stored in `localStorage` on your device only — there is no backend server, and nothing is ever sent anywhere except directly from your browser to the AI provider you chose.

## Known limitations

- Anthropic Claude and Groq do not support audio input at the API level — audio/ringtone files routed to them fall back to a conservative, filename-based guess rather than true audio analysis.
- OpenAI's audio understanding only accepts `.wav` and `.mp3` — other audio formats fall back to the filename-based guess when OpenAI is selected.
- Calling AI provider APIs directly from the browser means your API key is visible in your own browser's network tab. Only use this with keys you control, in a browser you trust.

## License

MIT — see [LICENSE](LICENSE).
