# 🔻 CHANGELOG – CRUNCHYROLL DOWNLOADER 🔻
## by Raim Ahmed

```

▄████  ██▓     ██▓ ▄████▄   ▄▄▄       ██▓     ██▓
 ██▒ ▀█▒▓██▒    ▓██▒▒██▀ ▀█  ▒████▄    ▓██▒    ▓██▒
▒██░▄▄▄░▒██░    ▒██▒▒▓█    ▄ ▒██  ▀█▄  ▒██░    ▒██░
░▓█  ██▓▒██░    ░██░▒▓▓▄ ▄██▒░██▄▄▄▄██ ▒██░    ▒██░
░▒▓███▀▒░██████▒░██░▒ ▓███▀ ░ ▓█   ▓██▒░██████▒░██████▒
░▒   ▒ ░ ▒░▓  ░░▓  ░ ░▒ ▒  ░ ▒▒   ▓▒█░░ ▒░▓  ░░ ▒░▓  ░
░   ░ ░ ░ ▒  ░ ▒ ░  ░  ▒     ▒   ▒▒ ░░ ░ ▒  ░░ ░ ▒  ░
░ ░   ░   ░ ░    ▒ ░░          ░   ▒     ░ ░     ░ ░
      ░     ░  ░ ░  ░ ░            ░  ░    ░  ░    ░  ░
░

```

All notable changes to this project are documented here.  
This project follows [Semantic Versioning](https://semver.org/).

---

## [1.1.0] – 2026-03-28
### Added by Raim Ahmed
- ✨ **Custom output folder** – now you can save MKVs anywhere (e.g., `/storage/emulated/0/Crunchrool Downloader`).
- 🧠 **Automatic CDM detection** – the tool picks up `.wvd` or `client_id.bin` + `private_key.pem` in the current directory.
- 🔧 **Verbose logging** option (`-v`) to help debugging.
- 📱 **Termux storage integration** – guide and commands for Android users.
- 🧪 **Tested and verified** with Chainsaw Man S01E01 (Hindi audio, 1080p).

### Changed
- 🎯 **Improved subtitle handling** – no more panic when `--subs-lang "none"` is used.
- 🚀 **Segment downloader** – now 10 workers instead of 5 (faster).
- 📦 **Batch download** – `--urls` now processes all URLs reliably.

### Fixed
- 🐛 **Panic on missing subtitle language** – resolved.
- 🔄 **Retry logic** – now properly handles connection resets.

---

## [1.0.0] – 2026-03-27
### Initial Release (based on CuteTenshii/crunchyroll-downloader)
- 🎬 **Download episodes or full seasons** from Crunchyroll.
- 🔊 **Multi‑audio** – supports any language (ja-JP, en-US, hi-IN, …).
- 📝 **Subtitles** – choose any language.
- 🔓 **Widevine L3 decryption** – works with `.wvd` or key files.
- ⚡ **Parallel segment downloads** – up to 10x faster.
- 🧩 **MKV output** with metadata (episode name, season, etc.).
- 📦 **Batch mode** – one URL per line in a text file.
- 🛡️ **Retry with backoff** – resilient to network glitches.
- 📱 **Termux ready** – full instructions for Android.

---

## 🧪 Upcoming (v1.2.0)
- [ ] **GUI mode** (maybe)
- [ ] **Custom chapter support**
- [ ] **Automatic CDM download** (safe and legal? We'll see…)
- [ ] **Better error messages** for revoked CDMs

---

## 🙌 Credits
- Original work by [CuteTenshii](https://github.com/CuteTenshii/crunchyroll-downloader) and contributors.
- Forked and enhanced by **Raim Ahmed** (hacker, anime lover, code whisperer).

---

## 📜 License
MIT – see [LICENSE](LICENSE) for details.

---

**Hack the planet, watch offline.** 🚀
