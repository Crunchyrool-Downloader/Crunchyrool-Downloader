# 🎬 Crunchyroll Downloader 🎬  
**by Raim**  

> Download anime from Crunchyroll in **Full HD**, with multi‑audio, subtitles, and automatic DRM decryption — all in a sleek MKV file.  
> *Hacker speed, anime lover’s heart.* 💀

[![GitHub stars](https://img.shields.io/github/stars/Crunchyrool-Downloader/Crunchyrool-Downloader?style=social)](https://github.com/Crunchyrool-Downloader/Crunchyrool-Downloader)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

## 🔥 Features

- 🎥 **Up to 1080p** video quality
- 🔊 **Any audio language** (Japanese, Hindi, English, …)
- 📝 **Subtitles in your language** – or none at all
- 🔓 **Widevine DRM decryption** – works with a `.wvd` or key pair
- ⚡ **10 parallel downloads** – segments fly down
- 🧩 **MKV with metadata** – episode names, season info, all embedded
- 📦 **Batch download** – one URL per line in a text file
- 🛡️ **Auto retry** – handles network glitches
- 📱 **Termux ready** – runs on your Android phone

---

## 🧰 Requirements

- **FFmpeg** (for merging audio/video/subtitles)
- **Crunchyroll Premium** (for premium content – no bypass)
- **Widevine CDM** – a `.wvd` file or `client_id.bin` + `private_key.pem`  
  (search `"ready to use cdms"` or extract from a rooted Android device)

---

## 📦 Installation

### From binary (easiest)
1. Grab the latest binary from the **Releases** tab.
2. Place it in a folder, e.g., `~/crunchyroll-downloader/`.

### Build from source (Termux)
```bash
pkg install golang ffmpeg git
git clone https://github.com/Crunchyrool-Downloader/Crunchyrool-Downloader.git
cd Crunchyrool-Downloader
go build .
```

---

🚀 Usage

Basic command:

```bash
./crunchyroll-downloader \
  --url "https://www.crunchyroll.com/watch/..." \
  --etp-rt "your_etp_rt_cookie" \
  --audio-lang "hi-IN" \
  --video-quality "1080p" \
  --output "/path/to/save/folder"
```

🍪 Get your etp_rt cookie

1. Log into Crunchyroll in a browser.
2. Open Developer Tools → Application (or Storage) → Cookies → https://www.crunchyroll.com
3. Copy the value of etp_rt.

🔓 Provide a Widevine CDM

Place a .wvd file (or client_id.bin + private_key.pem) in the same folder as the binary. The tool will detect it automatically.

📁 Output folder

By default, the MKV is saved in the current directory. Use --output to specify another location – perfect for your phone’s storage:

```bash
--output "/storage/emulated/0/Crunchrool Downloader"
```

---

🧪 Termux (Android) Example

After setting up and placing your CDM files:

```bash
termux-setup-storage
cd ~/crunchyroll-downloader
./crunchyroll-downloader \
  --url "https://www.crunchyroll.com/watch/G2XU040VQ/dog--chainsaw" \
  --etp-rt "ec0681fb-f10b-4bb6-9979-dd2b1dd00e9d" \
  --audio-lang "hi-IN" \
  --video-quality "1080p" \
  --output "/storage/emulated/0/Crunchrool Downloader"
```

Your anime will appear in Internal Storage / Crunchrool Downloader.

---

🧙‍♂️ Developer

Raim – coding, cracking, and crunching.
Built for the community, used with responsibility.

---

⚠️ Disclaimer

This tool is for educational purposes only. Only download content you have the legal right to access. Respect Crunchyroll’s terms of service. The developer is not responsible for any misuse.

---

🌟 Credits

Inspired by the work of CuteTenshii/crunchyroll-downloader and the amazing open‑source community.

---

📜 License

MIT – do whatever you want, just give credit.

---

Happy downloading! 🚀🍥

```

---

## What to do now

1. Go to your GitHub repo: `https://github.com/Crunchyrool-Downloader/Crunchyrool-Downloader`
2. Click on **README.md**.
3. Click the **pen icon** (Edit).
4. Replace the entire content with the text above.
5. Commit the change (you can use the default message).

Your repository will now show the proper documentation for the Crunchyroll downloader, with all the commands, explanations, and the output folder you wanted.

If you also want to upload the actual binary to the repo (e.g., in a `releases` section), you can do that later. But for now, the README is ready.
