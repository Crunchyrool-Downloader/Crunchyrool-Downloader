# 🔻 Crunchyroll Downloader – Developer Docs 🔻
## by Raim Ahmed

```

---

/ | |               | | ()               | |   | |     | |     | |
 | |    | | _ __ _   _   | |  _ _ __  _ __   _| |   | |   | | | | ___   ___ 
| |    | | '| | | |  | | | | ' \| ' \ / ` |   | | | | | __/ _ \ |/ _ \ / _ 
 | || || |  | || |  | | | | | | | | | | (| |   | | || | ||  __/ | () |  __/
\_|\_||   \_, |  || ||| ||| ||\_,|   |_|\_,|\_\___||\___/ \__|
/ |
                  |/

```

> **Peek under the hood – how we crack DRM, pull segments, and weave them into perfect MKVs.**  
> — *Raim Ahmed*

---

## 🧠 Architecture Overview

The tool is written in **Go** and follows a modular design. The main stages are:

1. **Authentication** – uses your `etp_rt` cookie to get a session token.
2. **Metadata fetch** – retrieves episode info, stream URLs, and license data.
3. **DRM decryption** – Widevine L3 decryption using a provided CDM.
4. **Segment downloading** – parallel fetching of audio/video chunks.
5. **Muxing** – merges everything into an MKV with FFmpeg.

---

## 📁 Code Modules

| File | Purpose |
|------|---------|
| `main.go` | Entry point, parses flags, orchestrates download |
| `drm.go` | Widevine license request, decryption setup |
| `episode.go` | Fetches episode metadata, streams, and subtitles |
| `season.go` | Handles season-level downloads (multiple episodes) |
| `mpd.go` | Parses MPD manifests, extracts segment URLs |
| `download.go` | Parallel segment downloader with retries |
| `output.go` | FFmpeg muxing, metadata injection |
| `token.go` | Session token retrieval using `etp_rt` |
| `http_request.go` | Reusable HTTP client with cookie handling |
| `utils.go` | Helper functions (progress, backoff, etc.) |

---

## 🔄 Download Flow (Step by Step)

1. **Parse input** – `--url` (single episode/season) or `--urls` (batch file).
2. **Get session token** – uses `etp_rt` to fetch a bearer token.
3. **Fetch episode list** (if season URL) → iterate over episodes.
4. **For each episode**:
   - Fetch episode details (title, number, description).
   - Retrieve the **MPD manifest URL** and **license server URL**.
   - Fetch the MPD, parse audio/video adaptations.
   - **Widevine license request** – using the CDM (`.wvd` or key files) to get decryption keys.
   - Download **video segments** in parallel (10 workers).
   - Download **audio segments** (if present) in parallel.
   - Download **subtitles** (if requested).
   - Use **FFmpeg** to merge into an MKV with metadata.
5. **Save to output folder** (default current dir, or `--output`).

---

## 🔓 Widevine DRM Decryption

Crunchyroll uses Widevine L3 (sometimes L1). The tool:

- Reads a **Widevine CDM** – either a `.wvd` file (which contains `client_id.bin` + `private_key.pem`) or the two separate files.
- Sends a license request to the license server using the **PSSH** from the MPD.
- Receives the **content keys** (decryption keys for audio/video).
- Uses those keys to decrypt each segment **on the fly** while downloading.

**Key files:**
- `client_id.bin` – device identification protobuf.
- `private_key.pem` – RSA private key for signing requests.
- `device.wvd` – a packed version of the above (pywidevine format).

The tool expects at least one of these in the current directory (or in a subfolder `device/`). It auto‑detects them.

---

## ⚡ Parallel Segment Downloader

The downloader spawns **10 goroutines** per stream (video/audio). Each worker:

- Pulls a segment URL from a channel.
- Downloads with retries and exponential backoff.
- Writes to a temporary file.
- After all segments are downloaded, merges them (concatenates).

This makes downloads **up to 10x faster** than sequential.

---

## 🎬 Muxing with FFmpeg

After all segments are downloaded (decrypted already), the tool:

- Builds an **FFmpeg command** with:
  - Input: the concatenated video segments (as a single file).
  - Input: the concatenated audio segments.
  - Optional: subtitles as a separate stream.
  - Metadata: episode title, season, episode number, etc.
  - Output: `.mkv` with chapters and tags.

The command is executed, and the final file is saved.

---

## 🛡️ Error Handling & Retries

- **Network errors** – retry with backoff (1s, 2s, 4s, … up to 5 tries).
- **Decryption failures** – abort and report CDM issues.
- **Segment download failures** – retry that segment individually.
- **FFmpeg errors** – exit with an error message.

---

## 🧪 Testing & Debugging

You can enable verbose logging with `-v` (if the tool supports it – the original did). The tool also prints progress (segment count) and final status.

For deeper debugging, run with `strace` or `gdb` (on Linux) to trace system calls.

---

## 🤝 Contributing

Want to hack on this? Feel free to:

1. Fork the repo.
2. Create a feature branch.
3. Make your changes (add new features, fix bugs).
4. Submit a pull request.

Please follow Go best practices and include comments for complex logic.

---

## 🧙‍♂️ Developer

**Raim Ahmed** – reverse engineer, Go enthusiast, and anime downloader connoisseur.  
This tool is the result of countless hours of tinkering with DRM, manifests, and FFmpeg.  
*Keep learning, keep hacking.*

---

## 📜 License

MIT – same as the original. Do whatever you want, just give credit where it's due.

---

**Now go fork it and make it even more awesome!** 🚀
