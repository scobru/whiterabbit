# 🐇 White Rabbit — a minimal Chitchatter clone

**P2P, end-to-end, serverless and account-free** chat in **a single file** (`index.html`), **zero build**, with just one real dependency: [Trystero](https://github.com/dmotz/trystero) (WebRTC + serverless signaling via BitTorrent trackers). Everything else is native browser APIs; `marked`, `dompurify` and `highlight.js` are only there to render markdown safely. All dependencies are loaded from a CDN via `importmap`.

Repo: [github.com/scobru/whiterabbit](https://github.com/scobru/whiterabbit)

## Run

You need a static server (ESM imports don't work from `file://`):

```bash
python -m http.server 5005
# then open http://localhost:5005
```

For real P2P, open the invite link in two different browsers/devices.

## Features (parity with Chitchatter)

- Multi-peer chat + **direct messages** (DMs targeted at a peer)
- **Markdown** (GFM) with **syntax highlighting** and multiline (Shift+Enter)
- **Backfill** of history to newcomers (in memory only)
- **Audio / video / screen sharing / livestream** (WebRTC)
- Encrypted **file sending** with a progress bar (automatic chunking)
- **Public** rooms (key = name) and **private** rooms (random id+secret in the link)
- **E2E**: WebRTC DTLS + encryption of the session descriptions with the room password
- **Peer verification** via public-key cryptography (ECDSA P-256 + fingerprint)
- **Client-side Moderation**: Mute & Block peers (hides messages, files, video streams and typing)
- **Browser Notifications & Audio Chime**: Native desktop notifications when receiving messages or files in background, with unread tab counter
- **Privacy / Streamer Mode**: Option to anonymize all nicknames
- **Mobile-friendly**: Responsive 2-tier compose box with full-width textarea and horizontal peer scroll
- **No message persistence** to disk (only name/color/theme/blocklist in localStorage)
- Light/dark themes
- Embeddable as a **Web Component**: `<chat-room room="name">` or `<chat-room room="id" secret="...">`

## The single trade-off of the single-file format

Files are kept in memory during transfer. For *truly* unlimited files with direct streaming to disk you'd need StreamSaver.js + a service worker (a second file), incompatible with the "single file" constraint. Everything else is at full parity.

## Stack comparison

| | Chitchatter | White Rabbit |
|---|---|---|
| UI | React + MUI | vanilla JS/CSS |
| Routing | React Router | `location.hash` |
| P2P | Trystero | Trystero |
| Markdown | react-markdown | marked + DOMPurify + highlight.js |
| Build | Vite | none |
| Name | Chitchatter | White Rabbit |
#