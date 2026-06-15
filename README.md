# Playback Translator

A single-file browser tool that live-translates Japanese game text from a [Epilogue GB Operator](https://epilogue.co/) Playback window into English. Point it at your Playback browser tab, crop in on the dialogue box, and it'll OCR and translate the text as it appears — no install, no build step, just open the HTML file.

## Features

- **Screen capture** via the browser's screen-sharing API — capture the Playback window/tab directly
- **Crop tool** to select just the dialogue box, improving OCR accuracy and cutting down on wasted scans
- **Live OCR** using [Tesseract.js](https://github.com/naptha/tesseract.js) (free, runs locally) with optional support for Google Cloud Vision or Claude Vision for higher accuracy
- **Translation** via MyMemory (free, 10k chars/day) or DeepL (with your own API key)
- **Claude Vision mode** — combines OCR and translation in a single call, with support for a custom glossary so names and terms stay consistent
- **Usage tracking** for whichever translator/OCR provider you're using, with daily/monthly limits shown in Settings
- **Light/dark themes**
- Adjustable scan interval and duplicate-frame detection to avoid re-translating unchanged text

## Usage

1. Open `index.html` in a modern browser (Chrome/Edge recommended for screen capture support)
2. Click **Capture Playback Window** and select the browser tab or window running GB Operator
3. Drag to draw a crop box around the dialogue area when prompted (or choose to scan full screen)
4. Translations appear in the feed as new Japanese text is detected on screen

### Settings (⚙)

- Choose your OCR engine: Tesseract (free/local), Google Cloud Vision, or Claude Vision
- Choose your translator: MyMemory or DeepL (requires API key + CORS proxy for DeepL)
- Add a glossary for consistent name/term translation (Claude Vision mode)
- Adjust the scan interval (1–10 seconds)

**Note:** API keys are entered directly in the browser and stored locally — hide the settings panel before screen sharing, and never commit your keys.

### Getting API keys

- **Google Cloud Vision** — Create a project in the [Google Cloud Console](https://console.cloud.google.com/), enable the Vision API, and create an API key under "Credentials". Requires a billing account to be attached, but the first 1,000 images/month are free. **Potential cost:** charges apply automatically beyond the free tier (~$1.50 per 1,000 images after that).
- **DeepL** — Sign up for a [DeepL API free account](https://www.deepl.com/pro-api) to get an API key (500,000 chars/month free). You'll also need a CORS proxy (e.g. a [Cloudflare Worker](https://workers.cloudflare.com/)) since DeepL's API doesn't allow direct browser calls. **Potential cost:** free tier should cover most use, but a paid DeepL plan is billed if you exceed it.
- **Anthropic Claude (Vision mode)** — Create an API key in the [Anthropic Console](https://console.anthropic.com/) under "API Keys". Requires a paid account with billing set up. **Potential cost:** real cost is incurred per scan (a small fraction of a cent each), which adds up over a long session — keep an eye on usage in the Console.
- **MyMemory** — No key required for the default free tier; optionally add your email in Settings to raise the daily limit to 10,000 characters.

## Requirements

- A modern browser with screen capture support (`getDisplayMedia`)
- No installation or dependencies — everything runs from the single `index.html` file (Tesseract.js is loaded from CDN)
- Optional: API keys for Google Cloud Vision, DeepL, and/or Anthropic Claude, depending on which engines you choose (see above — some of these can incur real costs)

## Known issues / in progress

- Crop preview aspect ratio can drift from the source video in some window sizes
- OCR accuracy on pixel fonts varies — Claude Vision generally performs best, Tesseract is the most limited

## Credits

Built for use with [Epilogue's GB Operator](https://epilogue.co/) Playback app.
