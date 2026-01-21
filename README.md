# StreamFlow — Advanced Web Video Player

StreamFlow is a high-performance, browser-based video player designed for **direct URLs, HLS (.m3u8), and DASH (.mpd)** streams. It focuses on aggressive buffering, precise seeking, playback control, and real-time network diagnostics. The frontend is framework-free, with an optional local proxy for bypassing CORS and referer restrictions.

---

## Features

- Direct video streaming via URL input or query parameters
- HLS and DASH playback support
- Smart buffering system:
  - Buffer-ahead tracking
  - History buffer awareness
  - Real-time network speed estimation
- Fully custom video controls:
  - Play / Pause
  - Seek via click, drag, keyboard
  - Skip ±10 seconds
  - Volume slider and mute
  - Playback speed control (0.25x → 100x)
  - Picture-in-Picture
  - Fullscreen
- Manual timestamp jump
- Keyboard shortcuts
- Visual buffer, loading, and error indicators
- Retry and fallback error handling
- Optional local proxy for blocked streams
- Supports signed / expiring HLS URLs (via proxy)

---

## Tech Stack

- HTML5 Video API
- Vanilla JavaScript (ES6+)
- CSS (custom UI)
- Optional libraries:
  - `hls.js` for HLS playback
  - `dash.js` for MPEG-DASH
  - Node.js for local proxy server

---

## Project Structure

```
├── index.html          # UI layout
├── style.css           # Player styling
├── play.js             # Core player logic
├── server.js           # (Optional) local proxy
├── vercel.json
└── README.md
```

---

## Running the Project

### Frontend

Serve the files using any static server.

Example using Live Server:

```
http://127.0.0.1:5500/index.html
```

---

## Loading Videos

### Option 1 — Paste URL
Paste a direct video, HLS, or DASH URL into the input field and press **Stream**.

### Option 2 — URL Parameters

Basic:

```
index.html?url=ENCODED_VIDEO_URL
```

Signed HLS URLs with additional parameters:

```
index.html?url=ENCODED_M3U8_URL&e=TOKEN&f=FLAG
```

The player reconstructs the full URL internally.

---

## CORS-Blocked Streams (Local Proxy)

Many platforms block cross-origin media playback. StreamFlow includes an optional local proxy to bypass these restrictions.

### Start the Proxy

```
node server.js
```

The proxy runs on:

```
http://localhost:4000
```

### Enable Proxy in UI

Enable the **Use Local Proxy** option in the player interface.

The player rewrites requests to:

```
http://localhost:4000/proxy?url=ENCODED_URL
```

### Proxy Capabilities

- Spoofs required headers (Referer, Origin, User-Agent)
- Supports binary streaming
- Forwards HTTP Range headers (required for seeking)
- Works with signed and expiring HLS URLs

---

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| Space / K | Play / Pause |
| F | Fullscreen |
| M | Mute |
| P | Picture-in-Picture |
| ← / J | Back 10 seconds |
| → / L | Forward 10 seconds |
| ↑ | Volume up |
| ↓ | Volume down |
| 0–9 | Jump to 0–90% |
| ? | Show shortcuts |

---

## Limitations

- DRM-protected streams are not supported
- Signed URLs expire and must be refreshed
- Proxy is required for strict CORS platforms
- Browsers may cap extreme playback speeds

---

## License

This project is provided for educational and experimental use only.
Ensure you have legal permission to stream any content you load.

---

## Credits

**Yashu Developer** — For This Project

**Maintained by SILENT GHOST** ⚡
