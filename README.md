# Faceless Video Generator — Guide & Documentation

**A local studio for avatar-fronted documentary YouTube videos — a HeyGen avatar, an ElevenLabs voiceover, and real internet footage or AI b-roll, assembled into one ready-to-upload MP4. Everything runs on your own computer.**

> 📦 You received the app as a **ZIP file** from your coach — this repository is the **documentation** for it. Start here:
>
> 📖 **Full step-by-step guide (no technical skills needed):** **[GUIDE-EN.md](./GUIDE-EN.md)**
> 🔄 **Already installed — how to update:** **[UPDATE.md](./UPDATE.md)**

---

## What it does

Paste a script. Pick a recurring **avatar** (created once from a single photo). ElevenLabs narrates the whole script, HeyGen brings your avatar to life lip-synced to that narration, and the rest of the screen is filled with **real footage / photos from across the internet** or **AI-generated b-roll** — your choice (AI / real / mix). Still images get a gentle Ken Burns zoom. Everything is stitched into one MP4 ready for YouTube. The app interface is **bilingual (English / French)** — toggle FR/EN in the top-right corner.

---

## Quick start (5 steps)

1. **Unzip** the app folder your coach sent you (put it wherever you like, e.g. Documents).
2. **Install two free programs once:** **Node.js 20+** (the "LTS" button at https://nodejs.org) and **FFmpeg** (on Windows you can simply drop ffmpeg's `bin` folder into the app folder — the app finds it automatically; on Mac: `brew install ffmpeg`).
3. **Install the app once:** double-click `install.command` (Mac) or `install.bat` (Windows).
   - *Mac: if it says "…is damaged and can't be opened", that's just macOS blocking a downloaded file — the [guide](./GUIDE-EN.md) has a 1-line fix (`xattr`).*
4. **Start it:** double-click `start.command` (Mac) or `start.bat` (Windows) → your browser opens at **http://localhost:3000**.
5. **Settings** → paste your **HeyGen + ElevenLabs + kie.ai** keys → **Save**. Then create an avatar and your first video.

> 💡 Most users should follow the friendly **[step-by-step guide](./GUIDE-EN.md)** — it covers everything: API keys, avatars, channels, costs, and troubleshooting.

---

## How it works

```
script
  │  ElevenLabs → voiceover + word timings
  ▼
beats (~N seconds each)
  ├─ avatar beats   → HeyGen renders your avatar for that beat
  └─ b-roll beats   → real footage / photos (Ken Burns zoom) or an AI clip
  ▼
everything is composited over the one voiceover → final.mp4
```

---

## A note on footage sources

The default footage sources (Pexels, Pixabay, Openverse, Wikimedia) are free for commercial use. A **YouTube** source is also available — by default it only uses **Creative-Commons** clips (lower copyright risk). You are responsible for what you publish.
