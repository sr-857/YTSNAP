# @sr-857/ytsnap

**YouTube Deep Link Generator** — Extract video IDs from YouTube URLs and generate native app deep links for iOS, Android, and web. Bypass in-app browser login walls on Instagram, TikTok, Twitter/X, Discord, WhatsApp, and anywhere else links are shared.

## Overview

Social media platforms trap external links inside sandboxed in-app browsers (webviews). These browsers are isolated from the native YouTube app's authentication state, forcing viewers to log in again before they can like, comment, or subscribe. YTSnap solves this by generating platform-aware deep links:

| Platform | Mechanism | Behavior |
|----------|-----------|----------|
| **iOS** | `youtube://` URI scheme | Intercepted by iOS, opens YouTube app directly. If app is absent, falls back to Safari. |
| **Android** | `intent://` URI with Intent extras | Android OS resolves the intent to the YouTube app. `browser_fallback_url` provides a graceful web fallback. |
| **Desktop** | Standard `https://` URL | Opens normally in the browser. No app switching needed on desktop. |

## Install

### Prerequisites

- Node.js >= 14.0.0
- A GitHub account authenticated to access [`@sr-857` packages](https://github.com/sr-857/YTSNAP/packages)

### Setup

```sh
# Configure npm to use GitHub Packages for the @sr-857 scope
echo "@sr-857:registry=https://npm.pkg.github.com" >> .npmrc

# Authenticate (classic PAT with read:packages scope)
echo "//npm.pkg.github.com/:_authToken=YOUR_GITHUB_TOKEN" >> .npmrc

npm install @sr-857/ytsnap
```

### Verify Installation

```js
const ytsnap = require('@sr-857/ytsnap');
console.log(ytsnap.extractId('https://youtu.be/dQw4w9WgXcQ'));
// 'dQw4w9WgXcQ'
```

## API Reference

---

### `extractId(input)`

Extracts a YouTube video ID from any supported URL format. This is the foundational function — all other functions depend on it.

#### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `input` | `string` | Yes | A YouTube URL (any format) or a raw 11-character video ID |

#### Returns

| Type | Condition |
|------|-----------|
| `string` | A valid 11-character video ID was found |
| `null` | No valid video ID could be extracted |

#### Supported URL Patterns

The function tests input against these regex patterns in order:

| # | Pattern | Example | Matches |
|---|---------|---------|---------|
| 1 | `/youtube\.com\/watch\?(?:.*&)?v=([a-zA-Z0-9_-]{11})/` | `https://www.youtube.com/watch?v=dQw4w9WgXcQ` | Standard watch page (with or without `www.`/`m.`) |
| 2 | `/youtu\.be\/([a-zA-Z0-9_-]{11})/` | `https://youtu.be/dQw4w9WgXcQ` | Short YouTube share links |
| 3 | `/youtube\.com\/embed\/([a-zA-Z0-9_-]{11})/` | `https://youtube.com/embed/dQw4w9WgXcQ` | Embedded player iframes |
| 4 | `/youtube\.com\/shorts\/([a-zA-Z0-9_-]{11})/` | `https://youtube.com/shorts/dQw4w9WgXcQ` | YouTube Shorts |
| 5 | `/youtube\.com\/v\/([a-zA-Z0-9_-]{11})/` | `https://youtube.com/v/dQw4w9WgXcQ` | Legacy video path |
| 6 | `/youtube\.com\/live\/([a-zA-Z0-9_-]{11})/` | `https://youtube.com/live/dQw4w9WgXcQ` | Live streams and premieres |
| 7 | Direct `[a-zA-Z0-9_-]{11}` match | `dQw4w9WgXcQ` | Raw video ID string |

#### Excluded Domains

| Domain | Reason |
|--------|--------|
| `music.youtube.com` | Music URLs use a different ID format and cannot be deep-linked |

#### Examples

```js
// Standard watch page
ytsnap.extractId('https://www.youtube.com/watch?v=dQw4w9WgXcQ');
// => 'dQw4w9WgXcQ'

// Mobile subdomain
ytsnap.extractId('https://m.youtube.com/watch?v=dQw4w9WgXcQ');
// => 'dQw4w9WgXcQ'

// With extra query parameters
ytsnap.extractId('https://youtube.com/watch?v=dQw4w9WgXcQ&t=30s&pp=ygUJcmlja2FzdGxleQ%3D%3D');
// => 'dQw4w9WgXcQ'

// Short URL
ytsnap.extractId('https://youtu.be/dQw4w9WgXcQ');
// => 'dQw4w9WgXcQ'

// Embed URL
ytsnap.extractId('https://youtube.com/embed/dQw4w9WgXcQ');
// => 'dQw4w9WgXcQ'

// Shorts
ytsnap.extractId('https://youtube.com/shorts/dQw4w9WgXcQ');
// => 'dQw4w9WgXcQ'

// Live stream
ytsnap.extractId('https://youtube.com/live/dQw4w9WgXcQ');
// => 'dQw4w9WgXcQ'

// Raw video ID
ytsnap.extractId('dQw4w9WgXcQ');
// => 'dQw4w9WgXcQ'

// Excluded: music.youtube.com
ytsnap.extractId('https://music.youtube.com/watch?v=dQw4w9WgXcQ');
// => null

// Invalid input
ytsnap.extractId('');
// => null

ytsnap.extractId('not a youtube url');
// => null

ytsnap.extractId(null);
// => null

ytsnap.extractId(undefined);
// => null

ytsnap.extractId(12345);
// => null (non-string input)
```

#### Edge Cases

| Input | Result | Explanation |
|-------|--------|-------------|
| `youtube.com/watch?feature=shared&v=VIDEO_ID` | `VIDEO_ID` | `v` param can appear anywhere in query string |
| `youtube.com/watch?v=` | `null` | Empty video ID is not matched |
| `youtube.com/shorts/VIDEO_ID?feature=share` | `VIDEO_ID` | Extra query params are ignored |
| `https://www.youtube.com/live/VIDEO_ID?si=abc123` | `VIDEO_ID` | Shorts-like tracking params don't interfere |
| `https://youtube.com` | `null` | No path, no ID |
| `https://youtu.be/` | `null` | No ID after short domain |
| `dQw4w9WgXcQ` with leading/trailing spaces | `dQw4w9WgXcQ` | Input is trimmed |

---

### `isValidYouTubeUrl(input)`

Checks whether a string contains a valid YouTube video URL. Pure convenience wrapper around `extractId`.

#### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `input` | `string` | Yes | The string to validate |

#### Returns

`boolean` — `true` if a valid video ID can be extracted, `false` otherwise.

#### Examples

```js
ytsnap.isValidYouTubeUrl('https://youtu.be/dQw4w9WgXcQ');
// => true

ytsnap.isValidYouTubeUrl('https://youtube.com/watch?v=dQw4w9WgXcQ');
// => true

ytsnap.isValidYouTubeUrl('garbage input');
// => false

ytsnap.isValidYouTubeUrl('');
// => false
```

---

### `generateLinks(videoId)`

Generates all platform-specific deep link variants for a given video ID. Use this to create the appropriate link for each target platform.

#### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `videoId` | `string` | Yes | A valid 11-character YouTube video ID |

#### Returns

| Property | Type | Value | Use Case |
|----------|------|-------|----------|
| `youtube` | `string` | `https://www.youtube.com/watch?v={id}` | Desktop browsers, fallback, email links |
| `ios` | `string` | `youtube://www.youtube.com/watch?v={id}` | iOS Universal Link — triggers YouTube app |
| `android` | `string` | `intent://...#Intent;...;end` | Android Intent — opens YouTube app natively |
| `web` | `string` | `https://www.youtube.com/watch?v={id}` | Alias for `youtube` — desktop fallback |

#### The Android Intent Explained

The Android deep link uses Chrome's Intent protocol:

```
intent://www.youtube.com/watch?v={id}#Intent;
  package=com.google.android.youtube;
  scheme=https;
  S.browser_fallback_url={encoded_fallback};
  end
```

| Component | Purpose |
|-----------|---------|
| `package=com.google.android.youtube` | Target app package name |
| `scheme=https` | URL scheme for the intent |
| `S.browser_fallback_url=...` | URL to open if the YouTube app is not installed |

#### Throws

| Condition | Error |
|-----------|-------|
| `videoId` is not exactly 11 characters of `[a-zA-Z0-9_-]` | `RangeError` |
| `videoId` is not a string | `RangeError` |

#### Examples

```js
// Basic usage
const links = ytsnap.generateLinks('dQw4w9WgXcQ');

links.youtube;
// => 'https://www.youtube.com/watch?v=dQw4w9WgXcQ'

links.ios;
// => 'youtube://www.youtube.com/watch?v=dQw4w9WgXcQ'

links.android;
// => 'intent://www.youtube.com/watch?v=dQw4w9WgXcQ#Intent;package=com.google.android.youtube;scheme=https;S.browser_fallback_url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DdQw4w9WgXcQ;end'

links.web;
// => 'https://www.youtube.com/watch?v=dQw4w9WgXcQ'

// Error handling
try {
  ytsnap.generateLinks('too_short');
} catch (err) {
  err.name;    // 'RangeError'
  err.message; // 'Invalid YouTube video ID: must be an 11-character string matching [a-zA-Z0-9_-]'
}
```

#### Platform Routing Logic

When using the generated links in a client-side app, route based on the user agent:

```js
function routeToYouTube(links) {
  const ua = navigator.userAgent;
  if (/iPhone|iPad|iPod/i.test(ua)) {
    window.location.href = links.ios;
  } else if (/Android/i.test(ua)) {
    window.location.href = links.android;
  } else {
    window.location.href = links.web;
  }
}
```

**Note on iOS behavior:** The `youtube://` scheme triggers the app immediately. If the YouTube app is not installed, iOS will show an error. A common pattern is to set a fallback timer — if the page doesn't lose visibility within ~2.5 seconds, redirect to the web URL.

---

### `buildRedirectUrl(videoId, baseUrl)`

Builds a redirect URL by appending `?v={videoId}` to a base URL. Use this to construct links for your own redirect service or landing page.

#### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `videoId` | `string` | Yes | A valid 11-character YouTube video ID |
| `baseUrl` | `string` | Yes | The base URL for the redirect (e.g., `https://ytsnap.com`) |

#### Returns

`string` — The base URL with `?v={videoId}` appended.

**URL cleaning behavior:**
- Existing query strings (`?foo=bar`) are stripped before appending `?v=`
- Hash fragments (`#section`) are stripped
- The function does NOT add or remove trailing slashes

#### Throws

| Condition | Error |
|-----------|-------|
| `videoId` is invalid | `RangeError` |
| `baseUrl` is empty or not a string | `RangeError` |

#### Examples

```js
// Simple base URL
ytsnap.buildRedirectUrl('dQw4w9WgXcQ', 'https://ytsnap.com');
// => 'https://ytsnap.com?v=dQw4w9WgXcQ'

// Base URL with trailing slash
ytsnap.buildRedirectUrl('dQw4w9WgXcQ', 'https://ytsnap.com/');
// => 'https://ytsnap.com/?v=dQw4w9WgXcQ'

// Base URL with existing params (stripped)
ytsnap.buildRedirectUrl('dQw4w9WgXcQ', 'https://ytsnap.com/?existing=param');
// => 'https://ytsnap.com?v=dQw4w9WgXcQ'

// Base URL with hash (stripped)
ytsnap.buildRedirectUrl('dQw4w9WgXcQ', 'https://ytsnap.com/#section');
// => 'https://ytsnap.com?v=dQw4w9WgXcQ'
```

#### Redirect Server Example

```js
// Node.js Express redirect handler
const express = require('express');
const ytsnap = require('@sr-857/ytsnap');

const app = express();

app.get('/go', (req, res) => {
  const { v } = req.query;

  if (!v || !ytsnap.isValidYouTubeUrl(v)) {
    return res.status(400).send('Invalid or missing video ID');
  }

  const id = ytsnap.extractId(v);
  const links = ytsnap.generateLinks(id);

  const ua = req.get('User-Agent') || '';

  if (/iPhone|iPad|iPod/i.test(ua)) {
    // iOS: fire youtube:// scheme with fallback
    res.send(`
      <script>
        window.location.href = '${links.ios}';
        setTimeout(function() {
          window.location.href = '${links.web}';
        }, 2500);
      </script>
    `);
  } else if (/Android/i.test(ua)) {
    res.redirect(links.android);
  } else {
    res.redirect(links.web);
  }
});
```

---

## Complete Example: Web App Integration

```html
<!DOCTYPE html>
<html>
<head>
  <title>YouTube Deep Link Generator</title>
</head>
<body>
  <input type="text" id="url-input" placeholder="Paste YouTube URL..." />
  <button onclick="generate()">Generate</button>
  <div id="output"></div>

  <script src="node_modules/@sr-857/ytsnap/index.js"></script>
  <script>
    function generate() {
      const input = document.getElementById('url-input').value;
      const id = ytsnap.extractId(input);

      if (!id) {
        document.getElementById('output').textContent = 'Invalid URL';
        return;
      }

      const links = ytsnap.generateLinks(id);
      document.getElementById('output').innerHTML = `
        <p><strong>iOS:</strong> <code>${links.ios}</code></p>
        <p><strong>Android:</strong> <code>${links.android}</code></p>
        <p><strong>Web:</strong> <code>${links.web}</code></p>
      `;
    }
  </script>
</body>
</html>
```

## Error Handling Reference

| Function | Invalid Input | Error Type | Message Pattern |
|----------|---------------|------------|-----------------|
| `extractId` | Non-string, empty, no match | No error (returns `null`) | — |
| `extractId` | `music.youtube.com` | No error (returns `null`) | — |
| `isValidYouTubeUrl` | Any | No error (returns `false`) | — |
| `generateLinks` | Invalid video ID | `RangeError` | `"Invalid YouTube video ID: must be an 11-character string matching [a-zA-Z0-9_-]"` |
| `generateLinks` | Non-string video ID | `RangeError` | Same as above |
| `buildRedirectUrl` | Invalid video ID | `RangeError` | `"Invalid YouTube video ID"` |
| `buildRedirectUrl` | Empty `baseUrl` | `RangeError` | `"baseUrl must be a non-empty string"` |

## Security Posture

| Vector | Mitigation |
|--------|------------|
| **Supply chain** | **Zero dependencies** — no `node_modules` to audit, no transitive risk |
| **Code injection** | No `eval`, no `Function()`, no dynamic `require()` — user input is never executed as code |
| **Input validation** | All inputs are type-checked. Video IDs are validated against a strict `[a-zA-Z0-9_-]{11}` regex before use. |
| **Network egress** | **No network calls** — the library is fully offline. No telemetry, no CDN fetches, no analytics. |
| **Prototype pollution** | Pure functions, no shared state, no object mutation |
| **Side effects** | None — all functions are deterministic and side-effect free |

## Internal Architecture

```
Input URL
    │
    ▼
extractId()
    │
    ├── Trim input
    ├── Check direct ID match (/^[a-zA-Z0-9_-]{11}$/)
    ├── Exclude music.youtube.com
    ├── Test 6 regex patterns in order
    └── Return ID or null
    │
    ▼
generateLinks(id)
    │
    ├── Validate ID (throws RangeError if invalid)
    ├── Build youtube URL
    ├── Build ios URI scheme
    ├── Build android intent URL
    └── Return { youtube, ios, android, web }
    │
    ▼
buildRedirectUrl(id, baseUrl)
    │
    ├── Validate ID
    ├── Validate baseUrl
    ├── Strip existing ?query and #hash
    └── Return baseUrl + ?v= + id
```

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | 2026-06-13 | Initial release. `extractId`, `isValidYouTubeUrl`, `generateLinks`, `buildRedirectUrl` |

## Performance

| Metric | Value |
|--------|-------|
| Bundle size | ~2.6 kB (packed), ~5.7 kB (unpacked) |
| Functions | 4 pure functions |
| Dependencies | 0 |
| `require()` time | < 1 ms |
| `extractId` throughput | ~500,000 ops/sec |
| `generateLinks` throughput | ~1,000,000 ops/sec |

## Compatibility

| Environment | Supported |
|-------------|-----------|
| Node.js >= 14 | ✅ |
| Node.js >= 18 | ✅ |
| Node.js >= 20 | ✅ |
| Browser (via `<script>` tag) | ✅ |
| Bun | ✅ |
| Deno | ✅ (via npm specifier) |
| TypeScript (no built-in types) | ⚠️ Use `// @ts-ignore` or declare module |

## Related

- [Web App](https://yt-snap.netlify.app/) — YTSnap online tool (no install needed)
- [GitHub Repository](https://github.com/sr-857/YTSNAP) — Source, issues, security policy
- [GitHub Packages](https://github.com/sr-857/YTSNAP/packages) — Published npm package

## License

All Rights Reserved. See [LICENSE.md](./LICENSE.md).
