<div align="center">

<img width="750" alt="YTSnap Logo" src="https://github.com/user-attachments/assets/9b3ffe92-cd20-48bb-8bb4-1f866325e8c9" />

<br/><br/>

# Open YouTube. In the App. Every Time.

### Stop losing engagement to sandboxed browsers.
### YTSnap turns any YouTube link into a native app deep link — instantly.

<br/>

[![Live](https://img.shields.io/badge/%F0%9F%9A%80%20LIVE-yt--snap.netlify.app-FF0000?style=for-the-badge)](https://yt-snap.netlify.app/)
[![npm](https://img.shields.io/badge/%F0%9F%93%A6%20npm-%40sr--857%2Fytsnap-CB3837?style=for-the-badge&logo=npm)](https://github.com/sr-857/YTSNAP/packages)
[![GitHub](https://img.shields.io/badge/%E2%AD%90%20SOURCE-sr--857%2FYTSNAP-181717?style=for-the-badge&logo=github)](https://github.com/sr-857/YTSNAP)

![](https://img.shields.io/badge/FREE-no%20signup-brightgreen?style=flat-square)
![](https://img.shields.io/badge/CLIENT--SIDE-no%20server-blue?style=flat-square)
![](https://img.shields.io/badge/TRACKING-none-lightgrey?style=flat-square)
![](https://img.shields.io/badge/ADS-none-orange?style=flat-square)

<br/>

<img width="700" alt="YTSnap Hero" src="https://github.com/user-attachments/assets/424101d3-370c-4711-8346-eaae6a80a5f7" />

</div>

---

## Table of Contents

- [The Problem](#the-problem)
- [How It Works](#how-it-works)
- [Supported Formats](#supported-formats)
- [Use It in 3 Steps](#use-it-in-3-steps)
- [npm Package](#npm-package----sr-857ytsnap)
- [Privacy-First Architecture](#privacy-first-architecture)
- [Who It's For](#who-its-for)
- [Contributing](#contributing)
- [License](#license)

---

## The Problem

When someone taps a YouTube link inside Instagram, WhatsApp, TikTok, or any other app — it opens in a **sandboxed in-app browser**. The viewer is not logged into Google. They cannot like, comment, or subscribe. You lose the engagement.

| ❌ Without YTSnap | ✅ With YTSnap |
|:---|:---|
| Opens in sandboxed in-app browser | Opens native YouTube app |
| User is **not logged in** | Session fully intact |
| Can't like · comment · subscribe | Full engagement enabled |
| Creator loses every conversion | Frictionless viewer experience |

---

## How It Works

```
Paste URL  →  Click SNAP  →  Copy link  →  Share anywhere  →  YouTube app opens
```

YTSnap detects the viewer's platform and fires the correct deep link scheme — entirely client-side, with no server involved.

| Platform | Deep Link Fired |
|:---|:---|
| 🍎 **iOS** | `youtube://www.youtube.com/watch?v={ID}` |
| 🤖 **Android** | `intent://www.youtube.com/watch?v={ID}#Intent;scheme=https;package=com.google.android.youtube;end` |
| 🖥️ **Desktop** | `https://www.youtube.com/watch?v={ID}` *(graceful fallback)* |

---

## Supported Formats

All four YouTube URL formats are parsed and deep linked automatically.

| Format | Example |
|:---|:---|
| Standard watch URL | `youtube.com/watch?v=dQw4w9WgXcQ` |
| Short URL | `youtu.be/dQw4w9WgXcQ` |
| Shorts | `youtube.com/shorts/dQw4w9WgXcQ` |
| Live stream | `youtube.com/live/dQw4w9WgXcQ` |

---

## Use It in 3 Steps

**① Paste** your YouTube URL at [yt-snap.netlify.app](https://yt-snap.netlify.app/)

**② Click SNAP** — deep link generated in milliseconds

**③ Share** — Instagram bio · TikTok · Twitter · WhatsApp · Discord · Email

---

## npm Package — `@sr-857/ytsnap`

Use YTSnap programmatically in your Node.js projects.
Published on [GitHub Packages](https://github.com/sr-857/YTSNAP/packages).

### Install

Configure your `.npmrc` to point the `@sr-857` scope at GitHub Packages:

```sh
echo "@sr-857:registry=https://npm.pkg.github.com" >> .npmrc
echo "//npm.pkg.github.com/:_authToken=YOUR_GITHUB_TOKEN" >> .npmrc
npm install @sr-857/ytsnap
```

> **Note:** A GitHub personal access token with at least `read:packages` scope is required to install from GitHub Packages.

### Quick Start

```js
const ytsnap = require('@sr-857/ytsnap');

// Extract a video ID from any YouTube URL
ytsnap.extractId('https://youtu.be/dQw4w9WgXcQ');
// => 'dQw4w9WgXcQ'

// Generate all deep link variants
ytsnap.generateLinks('dQw4w9WgXcQ');
// {
//   youtube: 'https://www.youtube.com/watch?v=dQw4w9WgXcQ',
//   ios:     'youtube://www.youtube.com/watch?v=dQw4w9WgXcQ',
//   android: 'intent://www.youtube.com/watch?v=dQw4w9WgXcQ#Intent;scheme=https;package=com.google.android.youtube;end',
//   web:     'https://www.youtube.com/watch?v=dQw4w9WgXcQ'
// }

// Validate a YouTube URL
ytsnap.isValidYouTubeUrl('https://youtube.com/watch?v=dQw4w9WgXcQ');
// => true

// Build a redirect URL
ytsnap.buildRedirectUrl('dQw4w9WgXcQ', 'https://yt-snap.netlify.app');
// => 'https://yt-snap.netlify.app?v=dQw4w9WgXcQ'
```

### API Reference

| Function | Parameters | Returns | Description |
|:---|:---|:---|:---|
| `extractId(input)` | `input: string` | `string \| null` | Extracts an 11-character video ID from any supported YouTube URL. Returns `null` if no valid ID is found. |
| `isValidYouTubeUrl(input)` | `input: string` | `boolean` | Returns `true` if the input is a recognizable YouTube video URL. |
| `generateLinks(videoId)` | `videoId: string` | `{ youtube, ios, android, web }` | Generates all platform-specific deep link variants for the given video ID. |
| `buildRedirectUrl(videoId, baseUrl)` | `videoId: string`, `baseUrl: string` | `string` | Appends `?v={videoId}` to the provided base URL to build a redirect-compatible link. |

For the complete API reference including parameter types, return types, edge cases, platform routing logic, error handling, performance benchmarks, and full integration examples, see [PACKAGE.md](./PACKAGE.md).

### Security

- **Zero external dependencies** — no supply chain risk
- **No network requests** — all processing is fully offline
- **Input validated** on every function call
- **No `eval`**, no dynamic `require`, no unsafe patterns

---

## Privacy-First Architecture

100% client-side JavaScript. Nothing is stored. Nothing is tracked. Ever.

| No Server | No Database | No Telemetry | No Cookies | No Ads | UTM-Safe |
|:---:|:---:|:---:|:---:|:---:|:---:|
| ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

UTM parameters and other query strings present in the original URL are preserved through the deep link generation process.

---

## Who It's For

**🎬 Creators** — Instagram bio links that open your video logged-in, ready to subscribe. Stop losing conversions to in-app browsers.

**📈 Marketers** — Email campaigns where mobile readers land in the app, not a stripped-down browser. Full engagement, zero friction.

**🏢 Agencies** — WhatsApp, Discord, and SMS campaigns that demand native-quality UX across every platform.

**🛠️ Developers** — Drop `@sr-857/ytsnap` into any Node.js app and deep link YouTube at the API level, zero dependencies.

---

## Contributing

Contributions, bug reports, and feature requests are welcome.

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m 'Add your feature'`
4. Push to the branch: `git push origin feature/your-feature`
5. Open a pull request

Please open an issue first for significant changes so we can discuss the approach.

---

## License

This project is open source. See [LICENSE](./LICENSE) for details.

---

<div align="center">

<img width="800" alt="YTSnap Twitter Card" src="https://github.com/user-attachments/assets/d07cd3a6-1a2e-40aa-b5f2-25874dcd0261" />

<br/><br/>

**Free · No Signup · No Tracking · No Ads · Client-Side Only**

[yt-snap.netlify.app](https://yt-snap.netlify.app/) &nbsp;·&nbsp; [npm](https://github.com/sr-857/YTSNAP/packages) &nbsp;·&nbsp; [GitHub](https://github.com/sr-857/YTSNAP)

</div>
