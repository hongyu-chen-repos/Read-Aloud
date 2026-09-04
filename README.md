# Read Aloud 🗣️

A completely free, offline, single-file web page that reads Word documents, plain text, Markdown, or anything you paste right in your browser. It packs support for 140+ languages and 400+ natural voices and accents. 🫶

No accounts, no uploads, no word limits, no subscriptions. Just open the page, drop in a file or paste your text, and hit Play. ✨


✨ What makes it great?

- Reads almost anything: Drop in .docx, .txt, or .md files, or just paste in emails, web articles, and random notes.
- A voice for every language: If your device has a voice for it, this tool can speak it. Microsoft Edge is the real MVP here, shipping with free natural voices in about 50 languages and tons of regional accents.
- Smart sentence detection: It handles punctuation rules for Latin, Cyrillic, Chinese, Japanese, Korean, Arabic, Hebrew, Devanagari, and even Spanish inverted punctuation seamlessly.
100% private: Everything is parsed right inside your browser. Nothing gets uploaded anywhere.
- Total control: The current sentence highlights as it reads. Click any sentence to jump to it. It even remembers where you left off across sessions.
- Pure and simple: One HTML file. Zero dependencies, zero build steps, zero tracking, zero cost.


🚀 Getting started

  1. Download index.html from this repo.
  2. Open it in any modern browser (Chrome, Edge, Firefox, or Safari 16.4+).
  3. Drag a .docx file onto the page, click to choose one, or just paste text.
  4. Hit Play!


💡 Voice quality tips

- Microsoft Edge is your best bet for human-sounding speech. It includes free, high-quality "Natural" voices in roughly 50 languages across any platform.
- Safari on Mac taps into the best Apple system voices. Want more? You can grab extra ones (including Siri) under System Settings > Accessibility > Spoken Content.
- Any device (Windows, macOS, iOS, Android) lets you install extra languages and voices in their speech or accessibility settings. This page will automatically find and list whatever you have available.


🔧 How it works

A .docx file is actually just a ZIP archive. This page digs into the archive's central directory, grabs word/document.xml, decompresses it using the browser's native DecompressionStream, and pulls out the text while ignoring deleted text and field codes. It then slices the text into sentences using a smart set of punctuation rules (covering Latin, Cyrillic, CJK, Korean, Arabic, Hebrew, Devanagari, and Spanish). Sentences that are way too long get chunked at clause boundaries.

Instead of dumping a whole document to the speech engine at once, it feeds sentences to speechSynthesis one by one. This allows for precise highlighting and navigation, and neatly avoids that annoying browser bug where long passages suddenly stop playing halfway through. Your reading position and settings are safely tucked away in localStorage.


💁🏻‍♀️ Honest limitations

- Real-time only: The Web Speech API doesn't expose an audio stream, so you can't export to an MP3.
Voice quality varies: How natural it sounds depends entirely on the voices built into your device.
- Legacy .doc isn't supported: You'll need to resave those as .docx first.
- Punctuation-free languages: Languages like Thai, which don't use sentence-ending punctuation, fall back to clause-length chunking.
- Old browsers: If your browser doesn't support DecompressionStream, you can't unpack .docx files (though pasted text will still work just fine).


🛠️ Customizing

Because everything lives in a single HTML file, there's no build step—just open it in a code editor and tweak away! Good places to start: the MAX chunk length in chunkLong, the abbreviation list in splitSentences, the voice ranking in voiceScore, keyboard shortcuts in init, and the CSS variables at the top for typography and colors.


📄 License

MIT. See LICENSE for details.
