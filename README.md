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

Paste a script. The app reads it out loud, cuts the narration into short shots, finds
something to show for each one — real footage from across the internet, an AI-generated
image or clip, or your recurring **presenter** (talking on camera, and optionally appearing
*inside* ordinary shots) — and stitches it all into one MP4 ready for YouTube. Still photos
get a gentle Ken Burns zoom. You can also skip the voice step and upload narration you
recorded yourself.

---

## You choose who does the work

The app isn't locked to any one company. A video needs a few jobs done, and you pick the
provider for each — **you only need keys for what you actually use**:

| The job | Your options | Required? |
|---|---|---|
| 🎙️ **The Voice** | ElevenLabs *(default)* · GenAIPro · AI84 · ai33.pro · Fish Audio · Hume AI · 69labs · HeyGen · MiniMax | **yes** — pick one, *or* upload your own narration |
| 🖼️ **The Pictures** | *Real:* Pexels · Storyblocks · Pixabay · Openverse · Wikimedia · Archive.org · YouTube · Web (Google) · Wigolo · Brave<br>*AI:* kie.ai *(default)* · 69labs · Magnific · Runware · Higgsfield | **yes** — at least one |
| 🧠 **The Brain** (picks what to show per sentence) | Google Gemini | **effectively yes — and API billing must be ON** |
| 👤 **The Presenter** | HeyGen (talking head) + your AI provider (the presenter inside shots) | **no** — skip it for a faceless video |
| ⏱️ **The Timer** | Groq Whisper | only when you **upload** narration; recommended for any voice except ElevenLabs |

⚠️ **Gemini does not fail loudly.** Without the key the app keeps running and searches your
sentence word-for-word, so the footage comes out literal and off-topic; on the free tier the
quota runs out mid-video and does the same thing. The app now tells you: a yellow box on the
Create page before you start, and a **"Completed with warnings — Gemini was not available"**
box on the finished run. A Google One / Gemini Advanced subscription does **not** count — it
must be **API** billing. Details in the [guide](./GUIDE-EN.md).

---

## Quick start (5 steps)

1. **Unzip** the app folder your coach sent you (anywhere, e.g. Documents).
2. **Install two free programs, once:** **Node.js 20+** (the "LTS" button at https://nodejs.org)
   and **FFmpeg** (Mac: `brew install ffmpeg`; Windows: drop ffmpeg's `bin` folder into
   `C:\Users\YOU\.faceless-studio\bin` — that folder survives updates, the app folder does not).
3. **Install the app once:** double-click `install.bat` (Windows) or `install.command` (Mac).
   - *Mac: if it says "…is damaged and can't be opened", that's just macOS blocking a
     downloaded file — the [guide](./GUIDE-EN.md) has a one-line fix (`xattr`).*
4. **Start it:** double-click `start.bat` / `start.command` → your browser opens at
   **http://localhost:3001**. Keep the black window open while you work.
5. **Settings** → pick your **voice** and **AI** provider, paste their keys, plus **Gemini**
   (billing on). Each key row has its own **Save**. Add **Pexels/Pixabay** for real footage, and
   **HeyGen** only if you want a presenter. Then make your first video.

> 🛡️ **The Create page checks your keys before anything is charged.** If the provider you
> picked has no key, a red box lists what is missing and the button stays off. Nothing is
> started — and nothing is billed — until that list is empty.

> 💡 Most people should just follow the friendly **[step-by-step guide](./GUIDE-EN.md)** —
> it covers keys, presenters, channels, costs, and what to do when something breaks.

---

## How it works

```
script  ── or an uploaded voiceover
  │  your chosen voice provider → narration + word timings
  ▼
shots (~N seconds each)  ── Gemini → what to show for each one
  ├─ presenter shots → HeyGen animates your avatar, lip-synced to that narration
  └─ visual shots    → real footage / photos (Ken Burns zoom), an AI image or clip,
                       or the presenter drawn inside the shot from his photo
  ▼
everything composited over the one narration → final.mp4
```

---

## Three things worth knowing before you start

**🛑 Don't let your computer sleep during a run.** A dark screen is fine; a *sleeping*
computer stops everything. It's the most common way a long run gets ruined — see §10 of
the [guide](./GUIDE-EN.md).

**🔄 If a run stops, Resume it — don't start over.** The app picks up where it left off and
reuses everything already generated, so you aren't charged twice — a presenter clip HeyGen
had already rendered is fetched, not re-ordered — see §11 of the [guide](./GUIDE-EN.md).

**📋 Read the box on a finished run.** "Completed with warnings" means the video exists but
is not what you asked for (no presenter, black beats, cut-off narration…). The box says what
fell short; "The video was not made" names the provider that stopped it and what to do.

---

## ⚠️ A note on footage sources

Pexels, Pixabay, Openverse, Wikimedia and Archive.org are free for commercial use, and
Storyblocks is licensed because you pay for it.

A **YouTube** source is **switched on by default** and sits first in the list. **It applies
no copyright filter** — it does not restrict itself to Creative-Commons clips. **Wigolo**,
**Web (Google)** and **Brave** are unfiltered open-web photos for the same reason. **You are
responsible for what you publish.** To turn any of them off: *Settings → Real footage → untick*
— the checkbox saves itself. Everything still works without them.
