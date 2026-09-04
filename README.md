# Read Aloud 🗣️

Read Aloud is a free, offline, single-file browser tool for reading `.docx`, `.txt`, `.md`, and pasted text. It supports 140+ languages and 400+ voices. No accounts, no uploads, no limits.

## ✨ Features
- **Broad File Support:** Drop `.docx`, `.txt`, `.md`, or paste text directly.
- **Multilingual Voices:** Supports all device-installed voices.
- **Smart Sentence Detection:** Handles punctuation rules for Latin, Cyrillic, CJK, Arabic, Hebrew, Devanagari, and Spanish.
- **100% Private:** All parsing occurs locally in the browser.
- **Interactive Reading:** Real-time sentence highlighting, click-to-jump navigation, and cross-session progress saving.
- **Zero Dependencies:** Single HTML file. No build steps, no tracking.

## 🚀 Getting Started
1. Download `index.html` from this repository.
2. Open in a modern browser (Chrome, Edge, Firefox, or Safari 16.4+).
3. Drag a file onto the page or paste text.
4. Click **Play**.

## 💡 Voice Quality Tips
- **Microsoft Edge:** Provides free, high-quality "Natural" voices in ~50 languages across all platforms.
- **Safari (macOS):** Uses Apple system voices. Add more via *System Settings > Accessibility > Spoken Content*.
- **Other Devices:** Install additional languages/voices in OS speech or accessibility settings. The tool auto-detects available voices.

## 🔧 How It Works
- **Docx Parsing:** Unzips `.docx` natively, extracts `word/document.xml`, decompresses via `DecompressionStream`, and extracts raw text while ignoring deletions and field codes.
- **Text Chunking:** Segments text by punctuation rules. Splits overly long sentences at clause boundaries.
- **Speech Synthesis:** Feeds sentences individually to `speechSynthesis` to enable precise highlighting and prevent browser playback cutoff bugs.
- **Storage:** Saves reading position and settings to `localStorage`.

## 💁🏻‍♀️ Limitations
- **No Audio Export:** Web Speech API restricts real-time audio stream extraction (no MP3 export).
- **Voice Dependency:** Voice quality depends entirely on pre-installed device voices.
- **No `.doc` Support:** Legacy `.doc` files must be resaved as `.docx`.
- **Punctuation-free Languages:** Languages like Thai fall back to clause-length chunking.
- **Browser Compatibility:** `.docx` parsing requires `DecompressionStream` support (pasted text works on all browsers).

## 🛠️ Customization
Edit `index.html` directly to adjust:
- `chunkLong`: Max chunk length.
- `splitSentences`: Abbreviation list.
- `voiceScore`: Voice ranking.
- `init`: Keyboard shortcuts.
- CSS variables: Typography and colors.

## 📄 License
MIT. See `LICENSE` for details.
