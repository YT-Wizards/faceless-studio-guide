# Faceless Video Generator — Guide & Documentation

**A local studio that turns a script into a finished YouTube video — narration, visuals, and an optional on-camera presenter, assembled into one ready-to-upload MP4. Everything runs on your own computer.**

> 📦 You received the app as a **ZIP file** from your coach — this repository is its **documentation**. Start here:
>
> 📖 **Full step-by-step guide (no technical skills needed):** **[GUIDE-EN.md](./GUIDE-EN.md)**
> 💳 **Paying for the services — read before your first video:** **[BILLING.md](./BILLING.md)**
> 🔄 **Already installed — how to update:** **[UPDATE.md](./UPDATE.md)**

> 📊 **Using the analytics app too?** Connecting Google for **YouTube Channel AI VIP** —
> including the third API most people miss, the one that unlocks thumbnail
> **click-through rate**: **[CHANNEL-AI-GOOGLE-SETUP.md](./CHANNEL-AI-GOOGLE-SETUP.md)**
> *(different product — nothing to do with making videos)*

---

## What it does

Paste a script. The app reads it out loud, cuts the narration into short scenes, finds
something to show for each one — real footage from across the internet, an AI-generated
image, or your recurring **presenter** talking on camera — and stitches it all into one
MP4 ready for YouTube. Still photos get a gentle Ken Burns zoom. The interface is
**bilingual (English / French)** — toggle FR/EN in the top-right corner.

---

## You choose who does the work

The app isn't locked to any one company. A video needs four jobs done, and you pick the
provider for each — **you only need keys for what you actually use**:

| The job | Your options | Required? |
|---|---|---|
| 🎙️ **The Voice** | ElevenLabs *(default)* · GenAIPro · 69labs · HeyGen · MiniMax | **yes** — pick one |
| 🖼️ **The Pictures** | *Real:* Pexels · Pixabay · Wikimedia · Openverse · Archive.org · YouTube<br>*AI:* kie.ai *(default)* · 69labs · Magnific | **yes** — at least one |
| 🧠 **The Brain** (picks what to show per sentence) | Google Gemini | **yes — and billing must be ON** |
| 👤 **The Presenter** | HeyGen | **no** — skip it for a faceless video |

⚠️ **Gemini is required, and its API billing must be enabled.** On the free tier the quota
runs out after a few scenes and your video comes out random — this is the single most
common cause of "it doesn't work". A Google One / Gemini Advanced subscription does **not**
count; it must be **API** billing. Details in the [guide](./GUIDE-EN.md).

---

## Quick start (5 steps)

1. **Unzip** the app folder your coach sent you (anywhere, e.g. Documents).
2. **Install two free programs, once:** **Node.js 20+** (the "LTS" button at https://nodejs.org)
   and **FFmpeg** (Windows: drop ffmpeg's `bin` folder into the app folder — it's found
   automatically; Mac: `brew install ffmpeg`).
3. **Install the app once:** double-click `install.bat` (Windows) or `install.command` (Mac).
   - *Mac: if it says "…is damaged and can't be opened", that's just macOS blocking a
     downloaded file — the [guide](./GUIDE-EN.md) has a one-line fix (`xattr`).*
4. **Start it:** double-click `start.bat` / `start.command` → your browser opens at
   **http://localhost:3000**.
5. **Settings** → paste **Gemini** (billing on) + your **voice provider's** key + **kie.ai**
   → **Save**. Add **Pexels/Pixabay** for real footage, and **HeyGen** only if you want a
   presenter. Then make your first video.

> 💡 Most people should just follow the friendly **[step-by-step guide](./GUIDE-EN.md)** —
> it covers keys, presenters, channels, costs, and what to do when something breaks.

---

## How it works

```
script
  │  your chosen voice provider → narration + word timings
  ▼
scenes (~N seconds each)
  ├─ presenter scenes → HeyGen animates your avatar, lip-synced to that narration
  └─ visual scenes    → real footage / photos (Ken Burns zoom) or an AI image/clip
  ▼
everything composited over the one narration → final.mp4
```

---

## Two things worth knowing before you start

**🛑 Don't let your computer sleep during a run.** A dark screen is fine; a *sleeping*
computer stops everything. It's the most common way a long run gets ruined — see §10 of
the [guide](./GUIDE-EN.md).

**🔄 If a run stops, Resume it — don't start over.** The app picks up where it left off and
reuses everything already generated, so you aren't charged twice — see §11 of the
[guide](./GUIDE-EN.md).

---

## ⚠️ A note on footage sources

Pexels, Pixabay, Openverse, Wikimedia and Archive.org are free for commercial use.

A **YouTube** source is **switched on by default** and sits first in the list. **It applies
no copyright filter** — it does not restrict itself to Creative-Commons clips. **You are
responsible for what you publish.** To turn it off: *full settings → `YT_DLP_ENABLED` → `0`
→ Save*. Everything still works without it.
