# @sr-857/ytsnap

**YouTube Deep Link Generator** — Extract video IDs from YouTube URLs and generate native app deep links for iOS, Android, and web.

## Install

```sh
# Configure npm to use GitHub Packages
echo "@sr-857:registry=https://npm.pkg.github.com" >> .npmrc
echo "//npm.pkg.github.com/:_authToken=YOUR_GITHUB_TOKEN" >> .npmrc

npm install @sr-857/ytsnap
```

## API Reference

---

### `extractId(input)`

Extracts a YouTube video ID from any supported URL format.

| Parameter | Type | Description |
|-----------|------|-------------|
| `input` | `string` | A YouTube URL or raw 11-character video ID |

**Returns:** `string | null` — the 11-character video ID, or `null` if no valid ID is found.

**Supported URL formats:**
- `youtube.com/watch?v={id}`
- `youtu.be/{id}`
- `youtube.com/embed/{id}`
- `youtube.com/shorts/{id}`
- `youtube.com/v/{id}`
- `youtube.com/live/{id}`
- Raw video ID string (11 characters)

**Note:** `music.youtube.com` URLs are explicitly excluded and return `null`.

```js
ytsnap.extractId('https://youtu.be/dQw4w9WgXcQ');
// => 'dQw4w9WgXcQ'

ytsnap.extractId('https://youtube.com/shorts/dQw4w9WgXcQ');
// => 'dQw4w9WgXcQ'

ytsnap.extractId('dQw4w9WgXcQ');
// => 'dQw4w9WgXcQ'

ytsnap.extractId('not a url');
// => null

ytsnap.extractId('');
// => null
```

---

### `isValidYouTubeUrl(input)`

Checks whether a string contains a valid YouTube video URL.

| Parameter | Type | Description |
|-----------|------|-------------|
| `input` | `string` | The string to validate |

**Returns:** `boolean`

```js
ytsnap.isValidYouTubeUrl('https://youtu.be/dQw4w9WgXcQ');
// => true

ytsnap.isValidYouTubeUrl('garbage input');
// => false
```

---

### `generateLinks(videoId)`

Generates all deep link variants for a given video ID.

| Parameter | Type | Description |
|-----------|------|-------------|
| `videoId` | `string` | An 11-character YouTube video ID |

**Returns:** `object` with the following properties:

| Property | Type | Description |
|----------|------|-------------|
| `youtube` | `string` | Standard `https://www.youtube.com/watch?v={id}` URL |
| `ios` | `string` | `youtube://` URI scheme for iOS |
| `android` | `string` | Android Intent URL that opens the YouTube app |
| `web` | `string` | Same as `youtube` — desktop fallback |

**Throws:** `RangeError` if the video ID is not a valid 11-character string.

```js
ytsnap.generateLinks('dQw4w9WgXcQ');
// {
//   youtube: 'https://www.youtube.com/watch?v=dQw4w9WgXcQ',
//   ios: 'youtube://www.youtube.com/watch?v=dQw4w9WgXcQ',
//   android: 'intent://www.youtube.com/watch?v=dQw4w9WgXcQ#Intent;package=com.google.android.youtube;scheme=https;S.browser_fallback_url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DdQw4w9WgXcQ;end',
//   web: 'https://www.youtube.com/watch?v=dQw4w9WgXcQ'
// }

ytsnap.generateLinks('bad');
// => RangeError: Invalid YouTube video ID
```

---

### `buildRedirectUrl(videoId, baseUrl)`

Builds a redirect URL by appending `?v={videoId}` to a base URL.

| Parameter | Type | Description |
|-----------|------|-------------|
| `videoId` | `string` | An 11-character YouTube video ID |
| `baseUrl` | `string` | The base URL for the redirect (e.g., `https://ytsnap.com`) |

**Returns:** `string` — the base URL with `?v={id}` appended. Existing query strings and hash fragments are stripped.

**Throws:** `RangeError` if the video ID is invalid or `baseUrl` is empty.

```js
ytsnap.buildRedirectUrl('dQw4w9WgXcQ', 'https://ytsnap.com');
// => 'https://ytsnap.com?v=dQw4w9WgXcQ'

ytsnap.buildRedirectUrl('dQw4w9WgXcQ', 'https://ytsnap.com/?page=1');
// => 'https://ytsnap.com?v=dQw4w9WgXcQ'
```

---

## Error Handling

All functions validate their input strictly. Invalid inputs produce a `RangeError` rather than silently failing or returning garbage data.

```js
try {
  ytsnap.generateLinks('short');
} catch (err) {
  err.name;    // 'RangeError'
  err.message; // 'Invalid YouTube video ID: must be an 11-character string...'
}
```

## Security

| Property | Guarantee |
|----------|-----------|
| Dependencies | **Zero** — no `npm install` risk |
| Network calls | **None** — fully offline |
| Input validation | **Strict** — all inputs checked |
| Code injection | **Immune** — no `eval`, no dynamic `require` |
| Surface area | **Minimal** — 4 pure functions, no state |

## License

All Rights Reserved. See [LICENSE.md](./LICENSE.md).
