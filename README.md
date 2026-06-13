<div align="center">

<br/>

<!-- Logo / Banner -->
<img src="https://cdn-icons-png.flaticon.com/512/1384/1384060.png" width="90" alt="YTSnap Logo"/>

<h1>
  <span style="color:#FF0000">YT</span>Snap
</h1>

<p><strong>⚡ Snap. Save. Stream.</strong><br/>
The fastest, cleanest YouTube downloader — supporting 4K, 1080p, 720p, MP3, and more.</p>

[![npm version](https://img.shields.io/npm/v/ytsnap?color=FF0000&label=npm&style=flat-square)](https://github.com/sr-857/YTSNAP/pkgs/npm/ytsnap)
[![License: MIT](https://img.shields.io/badge/license-MIT-brightgreen?style=flat-square)](LICENSE)
[![Node.js](https://img.shields.io/badge/node-%3E%3D16-blue?style=flat-square&logo=node.js)](https://nodejs.org)
[![Platform](https://img.shields.io/badge/platform-CLI%20%7C%20Web-lightgrey?style=flat-square)]()
[![Downloads](https://img.shields.io/badge/downloads-growing-orange?style=flat-square)]()
[![Stars](https://img.shields.io/github/stars/sr-857/YTSNAP?style=flat-square&color=yellow)](https://github.com/sr-857/YTSNAP)

<br/>

[🚀 Quick Start](#-quick-start) · [✨ Features](#-features) · [📖 API Reference](#-api-reference) · [🖥️ CLI Usage](#%EF%B8%8F-cli-usage) · [🤝 Contributing](#-contributing)

<br/>

</div>

---

## ✨ Features

| Feature | Details |
|---|---|
| 🎬 **Video Quality** | 4K Ultra HD · 1080p Full HD · 720p HD · 480p SD · 360p Low |
| 🎵 **Audio Extraction** | MP3 (high-quality audio-only) |
| 🔐 **No Auth Required** | No API keys, no login, no registration |
| 🌐 **Dual Mode** | Use as a CLI tool **or** as a programmatic library |
| 💾 **Custom Output** | Specify destination filename and directory |
| 🧼 **Zero Bloat** | Minimal dependencies, clean codebase |
| ⚡ **Fast** | Optimised download pipeline with progress reporting |

---

## 🚀 Quick Start

### Installation

```bash
# Install globally for CLI use
npm install -g ytsnap

# Or add to your project
npm install ytsnap
```

### As a CLI tool

```bash
# Download a video in 1080p
ytsnap --url "https://www.youtube.com/watch?v=dQw4w9WgXcQ" --quality 1080p

# Extract audio as MP3
ytsnap --url "https://www.youtube.com/watch?v=dQw4w9WgXcQ" --format mp3

# Download in 4K to a custom folder
ytsnap --url "https://youtu.be/dQw4w9WgXcQ" --quality 4k --output ./downloads
```

### As a Node.js library

```javascript
const ytsnap = require('ytsnap');

// Download a video
await ytsnap.download({
  url: 'https://www.youtube.com/watch?v=dQw4w9WgXcQ',
  quality: '1080p',
  output: './downloads'
});

// Extract audio only
await ytsnap.download({
  url: 'https://www.youtube.com/watch?v=dQw4w9WgXcQ',
  format: 'mp3',
  filename: 'my-song'
});
```

---

## 🖥️ CLI Usage

```
ytsnap [options]

Options:
  --url,     -u   YouTube video URL (required)
  --quality, -q   Video quality: 4k | 1080p | 720p | 480p | 360p  [default: "1080p"]
  --format,  -f   Output format:  mp4 | mp3                        [default: "mp4"]
  --output,  -o   Output directory                                 [default: ./]
  --filename     Custom filename (no extension)
  --help,    -h   Show help
  --version, -v   Show version number
```

### Examples

```bash
# Best quality video
ytsnap -u "https://youtu.be/VIDEO_ID" -q 4k

# Audio only — great for podcasts & music
ytsnap -u "https://youtu.be/VIDEO_ID" -f mp3 -o ~/Music

# Data-saver quality
ytsnap -u "https://youtu.be/VIDEO_ID" -q 360p

# Custom filename
ytsnap -u "https://youtu.be/VIDEO_ID" --filename "my-video" -o ./clips
```

---

## 📖 API Reference

### `ytsnap.download(options)`

Downloads a YouTube video or audio track.

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `url` | `string` | ✅ | — | Full YouTube video URL |
| `quality` | `string` | ❌ | `"1080p"` | `"4k"` · `"1080p"` · `"720p"` · `"480p"` · `"360p"` |
| `format` | `string` | ❌ | `"mp4"` | `"mp4"` or `"mp3"` |
| `output` | `string` | ❌ | `"./"` | Output directory path |
| `filename` | `string` | ❌ | Video title | Custom filename (without extension) |

**Returns:** `Promise<{ path: string, size: string, duration: string }>`

```javascript
const result = await ytsnap.download({
  url: 'https://www.youtube.com/watch?v=dQw4w9WgXcQ',
  quality: '1080p',
  output: './downloads',
  filename: 'rick-roll'
});

console.log(result);
// { path: './downloads/rick-roll.mp4', size: '42 MB', duration: '3:33' }
```

### `ytsnap.getInfo(url)`

Fetches metadata for a YouTube video without downloading.

```javascript
const info = await ytsnap.getInfo('https://www.youtube.com/watch?v=dQw4w9WgXcQ');

console.log(info);
// {
//   title: 'Rick Astley - Never Gonna Give You Up',
//   duration: '3:33',
//   author: 'Rick Astley',
//   availableQualities: ['4k', '1080p', '720p', '480p', '360p'],
//   thumbnail: 'https://...'
// }
```

---

## 🎯 Quality Guide

```
┌─────────────────────────────────────────────────────────┐
│  Quality      Resolution    Best For               Size  │
├─────────────────────────────────────────────────────────┤
│  4K           3840×2160     Large screens / TVs   ~600MB │
│  1080p ★      1920×1080     Everyday watching     ~150MB │
│  720p         1280×720      Balanced quality       ~80MB │
│  480p         854×480       Data saving            ~40MB │
│  360p         640×360       Minimal storage        ~20MB │
│  MP3          Audio only    Music / Podcasts        ~5MB │
└─────────────────────────────────────────────────────────┘
  ★ Recommended default
```

---

## ⚙️ Requirements

- **Node.js** v16 or higher
- **npm** v7+
- Internet connection

---

## 📦 Installation from GitHub Packages

This package is published to GitHub Packages under `@sr-857/ytsnap`. To install:

1. Create or update your `.npmrc` file in your project root:

```bash
@sr-857:registry=https://npm.pkg.github.com
```

2. Authenticate with GitHub Packages:

```bash
npm login --registry=https://npm.pkg.github.com
```

3. Install the package:

```bash
npm install @sr-857/ytsnap
```

---

## 🛠️ Development

```bash
# Clone the repository
git clone https://github.com/sr-857/YTSNAP.git
cd YTSNAP

# Install dependencies
npm install

# Run tests
npm test

# Link locally for CLI testing
npm link
ytsnap --help
```

---

## 🗺️ Roadmap

- [x] Video download (MP4) — 360p to 4K
- [x] Audio extraction (MP3)
- [x] CLI support
- [x] Programmatic API
- [ ] Playlist download support
- [ ] Progress bar with ETA
- [ ] Subtitle / caption download
- [ ] Format conversion (WebM, AAC, FLAC)
- [ ] Batch URL processing from `.txt` file

---

## 🤝 Contributing

Contributions are welcome! Here's how to get started:

1. **Fork** the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m 'Add amazing feature'`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a **Pull Request**

Please open an [issue](https://github.com/sr-857/YTSNAP/issues) first to discuss significant changes.

---

## 📄 License

Released under the **MIT License** — see [LICENSE](LICENSE) for details.

---

## ⚠️ Disclaimer

YTSnap is intended for **personal, educational, and offline use only**. Downloading copyrighted content without permission may violate YouTube's [Terms of Service](https://www.youtube.com/t/terms). The author assumes no liability for misuse.

---

<div align="center">

Made with ❤️ by [sr-857](https://github.com/sr-857)

⭐ **Star this repo** if YTSnap saved you time!

[![GitHub](https://img.shields.io/badge/GitHub-sr--857-181717?style=flat-square&logo=github)](https://github.com/sr-857)
[![Telegram](https://img.shields.io/badge/Community-Telegram-26A5E4?style=flat-square&logo=telegram)](https://t.me/ytsnapofficial)

</div>
