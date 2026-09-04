# Read Aloud 🗣️

A free, offline, single-file web page that reads Word documents, plain text, Markdown, or anything you paste out loud in your browser, with 140+ languages and 400+ natural voices and accents. . 🫶

No account. No upload. No word limit. No subscription. Open the page, drop in a file or paste some text, press Play.✨

**Highlights**

- Reads `.docx`, `.txt`, and `.md` files, and any pasted text (emails, web articles, notes, drafts)
- Speaks any language your device has a voice for; Microsoft Edge alone ships free natural voices in roughly 50 languages, from Afrikaans to Zulu, with many regional accents
- Sentence segmentation for most major writing systems, including Latin, Cyrillic, Chinese, Japanese, Korean, Arabic, Hebrew, Devanagari, and Spanish inverted punctuation
- Fully private: the document is parsed inside your browser and nothing is transmitted anywhere
- Sentence-by-sentence highlighting, click any sentence to jump, position remembered across sessions
- One HTML file, zero dependencies, zero build step, zero tracking, zero cost

## Features

- Reads `.docx` files directly, parsed entirely inside the browser
- Accepts `.txt` and `.md` files, and any pasted text
- Speaks every language your device has a voice for, typically dozens on a modern system
- Sentence-level control: the current sentence stays highlighted, and clicking any sentence starts playback from there
- Play, pause, previous, next, and restart controls
- Speed control (0.5× to 2×) and a ranked list of every available voice
- Per-document position memory across sessions
- Multilingual sentence segmentation, including mixed-language documents
- Keyboard shortcuts: Space toggles playback, arrow keys move between sentences
- Word count, progress bar, and an estimate of listening time remaining
- Light and dark themes following your system preference
- One HTML file, zero dependencies, zero network requests, zero tracking

## Getting started

1. Download `index.html` from this repository.
2. Open it in a current browser (Chrome, Edge, Firefox, or Safari 16.4 and later).
3. Drop a `.docx` file onto the page, or click to choose one, or paste text.
4. Press Play.

## Voice quality tips


- **Microsoft Edge** includes free high-quality "Natural" voices in roughly 50 languages on any platform and is the best choice for the most human-sounding output.
- **Safari on a Mac** exposes the best Apple system voices. Additional ones, including Siri voices, can be downloaded under System Settings, Accessibility, Spoken Content.
- **Windows, macOS, iOS, and Android** all allow extra languages and voices to be installed in their speech or accessibility settings, and the page will list whatever is available.

## How it works

A `.docx` file is a ZIP archive. The page locates `word/document.xml` by reading the archive's central directory, decompresses it with the browser's native `DecompressionStream`, and extracts the text runs while skipping deleted text and field codes. The text is then segmented into sentences using punctuation rules that cover Latin, Cyrillic, CJK, Korean, Arabic, Hebrew, Devanagari, and Spanish conventions, with overlong sentences chunked at clause boundaries. Sentences are sent to `speechSynthesis` one at a time, which enables per-sentence highlighting and navigation and also avoids the known browser defect where long utterances stop partway through. Reading position and settings are stored in `localStorage`.

## Limitations

- Playback is real-time only. The Web Speech API does not expose an audio stream, so the tool cannot export an MP3.
- Voice naturalness is bounded by the voices your device provides.
- Legacy binary `.doc` files are not supported; resave them as `.docx` first.
- Languages written without sentence-ending punctuation, such as Thai, fall back to clause-length chunking.
- Very old browsers without `DecompressionStream` cannot unpack `.docx` files, though pasted text still works.

## Customizing

Everything lives in one file, so changes are direct edits with no build step. Practical starting points include the `MAX` chunk length in `chunkLong`, the abbreviation list in `splitSentences`, the voice ranking in `voiceScore`, the keyboard shortcuts in `init`, and the CSS variables at the top for colors and typography.

## License

MIT. See [LICENSE](LICENSE).
