# Novel Reader

A single-page web app that reads your writing aloud. Paste a chapter, click any word, and it reads from there.

**Try it:** https://ghalebdweikat.github.io/novel-reader/

Or download [`index.html`](index.html) and open it in Chrome or Edge. It works the same as a local file.

## Features

- **Click to read from any word**, with the current sentence highlighted and kept in view
- **Play / pause / stop**, speed control (0.5×–2×), space bar toggles play/pause
- **Natural AI voices** via [Kokoro](https://huggingface.co/hexgrad/Kokoro-82M), running entirely in your browser. Nothing is sent to a server.
- **Built-in system voices** as an instant, zero-download alternative
- Remembers your text, position, speed and voice between visits (stored only in your browser)

## On phones

- Controls sit at the bottom within thumb reach; speed, voice and **Keep screen on** are in the ⚙ drawer
- Tap any word to read from exactly there
- **Built-in voices only.** The AI model needs more memory than mobile browsers give a tab. The page shows step-by-step instructions for downloading your phone's free high-quality voices (iPhone Premium/Enhanced voices, Google voices on Android).
- Browsers pause page audio when the screen locks, so keep the screen on while listening

## About the AI voices

On desktop, picking a Kokoro voice downloads the model once:

| Your machine | Runs on | Download | Speed |
|---|---|---|---|
| Has a GPU (WebGPU) | GPU | ~326 MB | Faster than real time; seamless playback |
| No GPU | CPU | ~90 MB | Slower than real time; short pauses between sentences |

After the first time it loads from your disk in about a second. Audio is generated a few sentences ahead while you listen. If a load ever crashes the tab, the page switches to a built-in voice next time instead of retrying.

## How it works

Everything is in `index.html`, with no build step and no dependencies to install.

- Text is split into sentences with `Intl.Segmenter`, with fixes for abbreviations (`Mr.`) and dialogue tags (`"Hi?" she said`).
- Built-in voices use the Web Speech API.
- Kokoro runs in a Web Worker through [kokoro-js](https://www.npmjs.com/package/kokoro-js), loaded from jsDelivr. Model files are cached in IndexedDB, because the Cache API can't store anything on `file://` pages.
- AI audio plays through the Web Audio API, which is what allows pausing mid-sentence.

## License

Apache-2.0. The Kokoro model and kokoro-js are also Apache-2.0.
