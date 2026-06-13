<div align="center">

<img width="750" alt="YTSnap Logo" src="https://github.com/user-attachments/assets/9b3ffe92-cd20-48bb-8bb4-1f866325e8c9" />

<br/><br/>

# **Open YouTube. In the App. Every Time.**

### **Stop losing engagement to sandboxed browsers.**  
### **YTSnap turns any YouTube link into a native app deep link — instantly.**

<br/>

[![Live](https://img.shields.io/badge/🚀%20LIVE-yt--snap.netlify.app-FF0000?style=for-the-badge)](https://yt-snap.netlify.app/)
[![npm](https://img.shields.io/badge/📦%20npm-%40sr--857%2Fytsnap-CB3837?style=for-the-badge&logo=npm)](https://github.com/sr-857/YTSNAP/packages)
[![GitHub](https://img.shields.io/badge/⭐%20SOURCE-sr--857%2FYTSNAP-181717?style=for-the-badge&logo=github)](https://github.com/sr-857/YTSNAP)

![](https://img.shields.io/badge/FREE-no%20signup-brightgreen?style=flat-square)
![](https://img.shields.io/badge/CLIENT--SIDE-no%20server-blue?style=flat-square)
![](https://img.shields.io/badge/TRACKING-none-lightgrey?style=flat-square)
![](https://img.shields.io/badge/ADS-none-orange?style=flat-square)

<br/>

<img width="700" alt="YTSnap Hero" src="https://github.com/user-attachments/assets/424101d3-370c-4711-8346-eaae6a80a5f7" />

</div>

---

<div align="center">

## **The Problem**

| ❌ Without YTSnap | ✅ With YTSnap |
|:---:|:---:|
| Opens in sandboxed in-app browser | Opens native YouTube app |
| User is **not logged in** | Session fully intact |
| Can't like · comment · subscribe | Full engagement enabled |
| Creator loses every conversion | Frictionless viewer experience |

</div>

---

<div align="center">

## **How It Works**

**`Paste URL`** &nbsp;→&nbsp; **`Click SNAP`** &nbsp;→&nbsp; **`Copy link`** &nbsp;→&nbsp; **`Share anywhere`** &nbsp;→&nbsp; **`YouTube app opens`**

<br/>

| Platform | Deep Link Fired |
|:---:|:---|
| 🍎 **iOS** | `youtube://www.youtube.com/watch?v={ID}` |
| 🤖 **Android** | `intent://...#Intent;scheme=https;package=com.google.android.youtube;end` |
| 🖥️ **Desktop** | `https://www.youtube.com/watch?v={ID}` *(graceful fallback)* |

</div>

---

<div align="center">

## **Supported Formats**

| Standard | Short URL | Shorts | Live |
|:---:|:---:|:---:|:---:|
| `youtube.com/watch?v=ID` | `youtu.be/ID` | `youtube.com/shorts/ID` | `youtube.com/live/ID` |

**All four formats. All deep linked. All native.**

</div>

---

<div align="center">

## **Use It In 3 Steps**

**① Paste** your YouTube URL at [yt-snap.netlify.app](https://yt-snap.netlify.app/)

**② Click SNAP** — deep link generated in milliseconds

**③ Share** — Instagram bio · TikTok · Twitter · WhatsApp · Discord · Email

</div>

---

<div align="center">

## **npm Package — `@sr-857/ytsnap`**

Use YTSnap programmatically in your Node.js projects.  
[Published on GitHub Packages](https://github.com/sr-857/YTSNAP/packages).

### Install

```sh
echo "@sr-857:registry=https://npm.pkg.github.com" >> .npmrc
echo "//npm.pkg.github.com/:_authToken=YOUR_GITHUB_TOKEN" >> .npmrc
npm install @sr-857/ytsnap
```

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
//   android: 'intent://www.youtube.com/watch?v=dQw4w9WgXcQ#Intent;...;end',
//   web:     'https://www.youtube.com/watch?v=dQw4w9WgXcQ'
// }

// Validate URLs
ytsnap.isValidYouTubeUrl('https://youtube.com/watch?v=dQw4w9WgXcQ');
// => true

// Build redirect URLs
ytsnap.buildRedirectUrl('dQw4w9WgXcQ', 'https://ytsnap.com');
// => 'https://ytsnap.com?v=dQw4w9WgXcQ'
```

For the full API reference, see [PACKAGE.md](./PACKAGE.md).

### Security

- **Zero external dependencies** — no supply chain risk
- **No network requests** — fully offline
- **Input validated** on every function
- **No `eval`**, no dynamic `require`

</div>

---

<div align="center">

## **Privacy-First Architecture**

| No Server | No Database | No Telemetry | No Cookies | No Ads | UTM-Safe |
|:---:|:---:|:---:|:---:|:---:|:---:|
| ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

**100% client-side JavaScript. Nothing is stored. Nothing is tracked. Ever.**

</div>

---

<div align="center">

## **Who It's For**

**🎬 Creators** — Instagram bio links that open your video logged-in, ready to subscribe.

**📈 Marketers** — Email campaigns where mobile readers land in the app, not a browser.

**🏢 Agencies** — WhatsApp, Discord & SMS campaigns that demand native-quality UX.

</div>

---

<img width="800" alt="YTSnap Twitter Card" src="https://github.com/user-attachments/assets/d07cd3a6-1a2e-40aa-b5f2-25874dcd0261" />

<br/><br/>

### **Free · No Signup · No Tracking · No Ads · Client-Side Only**

**[yt-snap.netlify.app](https://yt-snap.netlify.app/)** &nbsp;·&nbsp; **[npm](https://github.com/sr-857/YTSNAP/packages)** &nbsp;·&nbsp; **[GitHub](https://github.com/sr-857/YTSNAP)**

<br/>

</div>
