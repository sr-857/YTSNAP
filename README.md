<h1 style="text-align:center;">
  
  <img width="800" height="200" alt="logo-white" src="https://github.com/user-attachments/assets/9b3ffe92-cd20-48bb-8bb4-1f866325e8c9" />

# YTSnap — Documentation

> **YouTube Deep Link Generator & App Opener**  
> Version: v1 | Live at: [yt-snap.netlify.app](https://yt-snap.netlify.app/) | Source: [github.com/sr-857/YTSNAP](https://github.com/sr-857/YTSNAP)

---

<img width="600" height="400" alt="hero-illustration" src="https://github.com/user-attachments/assets/424101d3-370c-4711-8346-eaae6a80a5f7" />


## Table of Contents

1. [Overview](#overview)
2. [The Problem It Solves](#the-problem-it-solves)
3. [How It Works](#how-it-works)
4. [Features](#features)
5. [Usage Guide](#usage-guide)
6. [Supported URL Formats](#supported-url-formats)
7. [Platform-Specific Deep Link Behavior](#platform-specific-deep-link-behavior)
8. [Use Cases](#use-cases)
9. [Privacy & Security](#privacy--security)
10. [FAQ](#faq)
11. [Project Structure](#project-structure)
12. [Deployment](#deployment)
13. [Contributing](#contributing)
14. [License](#license)

---

## Overview

**YTSnap** is a free, client-side YouTube deep link generator built for content creators, digital marketers, and brand agencies. It converts any standard YouTube URL into a native app deep link — one that opens the YouTube mobile application directly instead of routing through a sandboxed in-app browser.

| Property | Value |
|---|---|
| Version | v1 |
| Live URL | https://yt-snap.netlify.app/ |
| Repository | https://github.com/sr-857/YTSNAP |
| Hosted on | Netlify |
| Processing | 100% client-side (no server, no database) |
| Cost | Free |
| Signup required | No |

---

## The Problem It Solves

When a standard YouTube URL (e.g. `https://youtube.com/watch?v=abc123`) is shared on social platforms like Instagram, TikTok, Twitter/X, or Discord, mobile operating systems route the tap into that platform's **in-app browser** — a sandboxed webview isolated from the device's official app ecosystem.

This creates a critical friction point for creators:

- The viewer is **not logged in** inside the in-app browser (cookies are isolated).
- Without being logged in, they **cannot like, comment, or subscribe**.
- The creator loses meaningful engagement from every such tap.

**YTSnap eliminates this friction** by generating a link that triggers the OS to launch the native YouTube application directly, keeping the viewer's session intact and fully engaged.

---

## How It Works

YTSnap operates entirely in the browser through three steps:

```
1. Parse    →  Extract the YouTube video ID from the pasted URL
2. Generate →  Build a platform-aware deep link URI
3. Redirect →  On tap, fire the URI scheme to launch the native app
```

### Deep Link URI Schemes Used

| Platform | URI Scheme |
|---|---|
| iOS | `youtube://www.youtube.com/watch?v={VIDEO_ID}` |
| Android | Android Intent: `intent://www.youtube.com/watch?v={VIDEO_ID}#Intent;scheme=https;package=com.google.android.youtube;end` |
| Desktop (fallback) | Standard `https://www.youtube.com/watch?v={VIDEO_ID}` |

The redirect page reads the visitor's **User-Agent** at runtime to determine which URI scheme to fire, ensuring the correct behavior on every device.

---

## Features

- **Instant deep link generation** — paste a URL, click SNAP, get a shareable link in seconds.
- **Cross-format support** — handles standard videos, YouTube Shorts, and Live Streams.
- **Platform-aware routing** — detects iOS vs. Android vs. desktop and fires the appropriate URI.
- **Zero server dependency** — all logic runs client-side; no data is sent to any server.
- **No tracking or telemetry** — YTSnap does not log, store, or monitor any links generated.
- **UTM-parameter safe** — because there are no link wrappers or server-side redirects, external tracking parameters are fully preserved.
- **Ad-free** — no intermediate ads shown to the viewer clicking the link.
- **No signup required** — use it immediately without creating an account.

---

## Usage Guide

### Step 1 — Paste Your YouTube URL

Open [yt-snap.netlify.app](https://yt-snap.netlify.app/) and paste any valid YouTube video URL into the input field. Accepted formats include:

```
https://www.youtube.com/watch?v=dQw4w9WgXcQ
https://youtu.be/dQw4w9WgXcQ
https://www.youtube.com/shorts/abc123
https://www.youtube.com/live/xyz789
```

### Step 2 — Click SNAP

Press the **SNAP** button. YTSnap will parse the video ID from your URL and generate a unique shareable deep link.

> If the URL does not contain a valid YouTube video ID, an error message will appear: `couldn't find a valid YouTube video ID`.

### Step 3 — Copy & Share

Click **COPY** to copy the generated link to your clipboard. Share this link anywhere:

- Instagram Bio or Story link sticker
- TikTok profile link
- Twitter/X post
- Discord server or DM
- WhatsApp message
- Email newsletter

### Step 4 — Viewer Experience

When a viewer taps the YTSnap link on their mobile device, the page instantly fires the YouTube app URI scheme. The native YouTube app opens directly — no in-app browser, no login wall, no friction.

---

## Supported URL Formats

YTSnap uses regex-based parsing to extract video IDs from all major YouTube URL patterns:

| URL Pattern | Example |
|---|---|
| Standard watch URL | `youtube.com/watch?v=VIDEO_ID` |
| Short URL | `youtu.be/VIDEO_ID` |
| Shorts | `youtube.com/shorts/VIDEO_ID` |
| Live stream | `youtube.com/live/VIDEO_ID` |

All four formats produce a valid deep link that correctly routes to the video, short, or stream inside the native app.

---

## Platform-Specific Deep Link Behavior

### iOS

YTSnap fires the `youtube://` custom URL scheme registered by the official YouTube app. If the YouTube app is installed, iOS immediately opens it. If not, the browser falls back to the standard HTTPS URL.

### Android

YTSnap fires an **Android Intent URL**, which passes the request to the Android Intent resolution system. If the YouTube app is installed and set as the default handler, it opens immediately. Otherwise, the user is prompted to select an app or falls back to the browser.

### Desktop

On desktop browsers where no native app URI scheme is applicable, YTSnap falls back gracefully to the standard `https://www.youtube.com/...` URL, ensuring the link always works.

---

## Use Cases

### Content Creators

- Add the YTSnap link in your **Instagram bio** so followers open your latest video in the YouTube app — logged in and ready to subscribe.
- Use it in **Instagram Story link stickers** to drive higher engagement rates.
- Share new video announcements in **TikTok DMs** with a link that opens YouTube natively.

### Digital Marketers

- Embed YTSnap links in **email newsletters** to ensure mobile readers are taken directly into the YouTube app.
- Use alongside **UTM parameters** for campaign tracking — YTSnap does not interfere with external analytics.
- Reduce drop-off in conversion funnels driven from social media ads.

### Brand Agencies

- Use in **Discord** community announcements so members can open brand videos without leaving the native app.
- Embed in **WhatsApp broadcast messages** for influencer or product launch campaigns.
- Apply in **SMS marketing** where mobile-native experiences are critical.

---

## Privacy & Security

YTSnap is designed with a privacy-first architecture:

- **No server-side processing.** All deep link generation happens entirely inside the visitor's browser using JavaScript.
- **No database.** No links, video IDs, or user data are stored anywhere.
- **No telemetry.** YTSnap does not collect click data, user-agent data, or any analytics about generated links.
- **No cookies.** YTSnap sets no tracking cookies on the generator page.
- **No intermediate ad pages.** Competitors often interpose an ad view before redirecting; YTSnap fires the deep link directly.

This makes YTSnap safe for use in affiliate marketing, sponsorships, and brand campaigns where link integrity and viewer trust are important.

---

## FAQ

**Does YTSnap work for YouTube Shorts?**  
Yes. Shorts URLs (`youtube.com/shorts/...`) are parsed correctly and generate valid deep links that open the Shorts view in the native app.

**Does it work for YouTube Live Streams?**  
Yes. Live stream URLs (`youtube.com/live/...`) are supported and generate correct URI redirects.

**Will the deep link always open the app?**  
The deep link fires the native URI scheme; if the YouTube app is installed on the viewer's device, it will open. If the app is not installed, the device falls back to opening the URL in the browser.

**Does YTSnap conflict with UTM parameters or affiliate tracking?**  
No. Because there is no server-side link wrapper, all query parameters (including UTMs and affiliate codes) attached to the YTSnap redirect URL are preserved end-to-end.

**Is YTSnap free to use?**  
Yes, completely free with no signup required.

**Why does the link go to a YTSnap page before opening YouTube?**  
YTSnap needs a web page context to read the visitor's User-Agent and execute the appropriate URI scheme. This intermediate page is lightweight and fires the deep link instantly upon load — the viewer typically sees just the "OPENING YOUTUBE — Launching app instantly..." message for a fraction of a second.

**Is my data safe?**  
Yes. No data about you or your viewers is collected, stored, or transmitted. All processing is client-side.

---

## Project Structure

```
YTSNAP/
├── README.md          # Repository readme
└── ...                # Source files (HTML, CSS, JS)
```

The project is a static web application deployed on Netlify. No backend, build pipeline dependencies, or database is required.

---

## Deployment

YTSnap is deployed as a **static site on Netlify**.

To deploy your own fork:

1. Fork the repository: [github.com/sr-857/YTSNAP](https://github.com/sr-857/YTSNAP)
2. Log in to [netlify.com](https://netlify.com) and click **Add new site → Import an existing project**.
3. Connect your GitHub account and select the forked repository.
4. Configure build settings (none required for a static site — leave build command blank).
5. Click **Deploy site**.

Netlify will assign a public URL. You can add a custom domain from the Netlify dashboard under **Domain settings**.

---


## Contributing

Contributions are welcome. To contribute:

1. Fork the repository on GitHub.
2. Create a feature branch: `git checkout -b feature/your-feature-name`
3. Make your changes and commit: `git commit -m "Add your feature"`
4. Push to your fork: `git push origin feature/your-feature-name`
5. Open a **Pull Request** against the `main` branch of [sr-857/YTSNAP](https://github.com/sr-857/YTSNAP).

Please ensure any changes maintain the client-side-only, no-tracking architecture of the project.

---

## License

No license is currently specified in the repository. All rights are presumed to be reserved by the author ([sr-857](https://github.com/sr-857)) unless stated otherwise. Contact the repository owner for usage permissions.

---

*Documentation generated for [yt-snap.netlify.app](https://yt-snap.netlify.app/) · Repository: [github.com/sr-857/YTSNAP](https://github.com/sr-857/YTSNAP)*



<img width="1200" height="675" alt="twitter-card" src="https://github.com/user-attachments/assets/d07cd3a6-1a2e-40aa-b5f2-25874dcd0261" />


</h1>
