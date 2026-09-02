# Read Aloud 🗣️

A free, offline, single-file web page that reads Word documents, plain text, Markdown, or anything you paste out loud in your browser. 🫶

No account. No upload. No word limit. No subscription. Open the page, drop in a file or paste some text, press Play.✨

**Highlights**

- Reads `.docx`, `.txt`, and `.md` files, and any pasted text (emails, web articles, notes, drafts)
- Speaks any language your device has a voice for; Microsoft Edge alone ships free natural voices in roughly 50 languages, from Afrikaans to Zulu, with many regional accents
- Sentence segmentation for most major writing systems, including Latin, Cyrillic, Chinese, Japanese, Korean, Arabic, Hebrew, Devanagari, and Spanish inverted punctuation
- Fully private: the document is parsed inside your browser and nothing is transmitted anywhere
- Sentence-by-sentence highlighting, click any sentence to jump, position remembered across sessions
- One HTML file, zero dependencies, zero build step, zero tracking, zero cost

## Why this exists

Listening to a document is one of the most effective ways to review it, yet most online text-to-speech services put this basic capability behind word limits, file-upload requirements, and monthly subscriptions. At the same time, every modern browser already ships with a complete speech engine through the Web Speech API, and every modern browser can decompress ZIP data natively. A `.docx` file is simply a ZIP archive containing XML. All the pieces needed to read a document aloud already exist on your computer, for free. This project connects them in a single HTML file with no server, no dependencies, and no build step.

## What it can do for you

**Listen to anything, not just Word files.** Beyond `.docx`, `.txt`, and `.md` files, the paste box accepts arbitrary text, so an email you are about to send, an article copied from the web, meeting notes, or a chapter of a draft can all be read back to you in seconds.

**Hear your own writing.** Listening exposes awkward phrasing, repeated words, missing words, and rhythm problems that silent re-reading tends to skip over. Writers, students, and researchers can run a full draft through their ears before submitting it.

**Get through long documents without staring at a screen.** Load a report, a thesis chapter, or a contract and listen while you take notes, rest your eyes, or do something else with your hands. A progress bar and a listening-time estimate show how much remains.

**Work in many languages.** The tool speaks any language your device or browser provides a voice for. Microsoft Edge includes free natural voices covering roughly 50 languages with many regional accents, and Windows, macOS, iOS, and Android all allow additional languages to be installed in their speech settings. The sentence splitter understands the punctuation conventions of most major writing systems, with guards for English abbreviations such as "Dr." and decimals such as "3.14", full support for Chinese 。！？, and correct handling of Arabic ؟, Devanagari ।, and Spanish ¿¡. Mixed-language documents read correctly, and the voice list is ranked to match the document's language.

**Support different ways of reading.** Sentence-by-sentence highlighting pairs audio with text, which helps readers with dyslexia, visual fatigue, or attention difficulties follow along. Adjustable speed from 0.5× to 2× serves both careful listeners and fast reviewers, and language learners can slow difficult passages down and replay any sentence with a click.

**Keep your place in long documents.** Reading position is saved per document, so a book-length file can be continued days later exactly where you stopped.

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

## Why it matters

**Your documents stay yours.** The file is parsed in memory, in your browser, on your machine. Nothing is transmitted anywhere, which makes the tool suitable for confidential material such as contracts, medical documents, and unpublished manuscripts. You can verify this claim by reading the source, or by loading a document with the network disconnected.

**It is software you can keep.** There is no service that can shut down, no pricing that can change, and no API key that can expire. The file works offline today and will work offline in ten years.

**It is small enough to understand.** The entire tool is a few hundred lines in one file. Anyone with basic web knowledge can read every line, confirm what it does, and change what they dislike.

**It is built only on open standards.** ZIP, OOXML, the Web Speech API, and the Compression Streams API are all publicly documented. Nothing proprietary is involved, so nothing can be taken away.

## Getting started

1. Download `index.html` from this repository.
2. Open it in a current browser (Chrome, Edge, Firefox, or Safari 16.4 and later).
3. Drop a `.docx` file onto the page, or click to choose one, or paste text.
4. Press Play.

### Host it yourself (optional)

Enable GitHub Pages on this repository and the tool becomes a URL you can open from any device, including a phone. It remains fully client-side; documents are still processed only on the device that opens the page.

## Voice quality tips

Voices come from your browser and operating system, not from this tool.

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
