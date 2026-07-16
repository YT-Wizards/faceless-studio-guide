# Faceless Video Generator — the complete guide

> **For everyone. No technical skills needed.**
> You paste a script. The app builds a finished YouTube video — narration, visuals,
> and (optionally) a presenter on camera. Everything runs **on your own computer**.

---

## 1. What actually happens (in 30 seconds)

```
        Your script (plain text)
                 │
                 ▼
   1. A VOICE reads it out loud                    → the narration
                 │
                 ▼
   2. The app cuts the narration into short "scenes"
      (a few seconds each, following the voice's timing)
                 │
                 ▼
   3. For every scene, it finds something to show
      • real footage from the internet, and/or
      • an AI-generated image or video
      • now and then → your PRESENTER talks on camera (optional)
                 │
                 ▼
   4. Everything is glued into one MP4, ready to upload
```

---

## 2. The four jobs — and you choose who does each

This is the most important page in this guide. **The app doesn't force you onto any
particular company.** A video needs four jobs done, and for each one you pick who does it:

| # | The job | What it means | Do I need it? |
|---|---|---|---|
| 🎙️ | **The Voice** | reads your script out loud | **Yes** — pick one |
| 🖼️ | **The Pictures** | what's on screen while the voice talks | **Yes** — pick at least one |
| 🧠 | **The Brain** | decides *what to show* for each sentence | **Yes** — required |
| 👤 | **The Presenter** | a person on camera, now and then | **No** — optional |

You only pay for the ones you use. **You do not need every key in this guide.**

### 🎙️ The Voice — pick ONE

| Option | You need | Notes |
|---|---|---|
| **ElevenLabs** | an ElevenLabs key | **the default** — the best known, huge voice library. Click **"Load voices"** to pick one from a list. |
| **GenAIPro** | a GenAIPro key | an ElevenLabs reseller — same voices, different billing |
| **69labs** | a 69labs key | ElevenLabs / EdgeTTS / voice cloning, all through one gateway |
| **HeyGen** | a HeyGen key | convenient if you already use HeyGen for a presenter. Also has a **"Load voices"** picker. |
| **MiniMax** | a MiniMax key **+ Group ID** | cheap, good quality, supports voice cloning |

Set it in **Settings → Voice provider**. The page then shows the key field for the
provider you picked, plus its voice field — you don't need the other providers' keys.

### 🖼️ The Pictures — pick at least one source

**Real footage** (photos and video clips from the internet):

| Source | Key needed? | What you get |
|---|---|---|
| **Pexels** | yes (free to get) | good stock video + photos |
| **Pixabay** | yes (free to get) | good stock video + photos |
| **Wikimedia** | **no key** | historical/archive photos |
| **Openverse** | **no key** | freely-licensed photos |
| **Archive.org** | **no key** | old archive footage |
| **YouTube** | no key, but ⚠️ see §9 | real clips from YouTube |

**AI-generated pictures** (when no good real footage exists, or if you prefer AI):

| Option | You need |
|---|---|
| **kie.ai** | a kie.ai key — *this is the default* |
| **69labs** | a 69labs key |
| **Magnific** | a Magnific key |

> 💡 **You'll usually want both**: real footage first, AI as the backup for scenes
> where nothing real fits. That's what "Mix" mode does.

### 🧠 The Brain — required

**Google Gemini** reads each sentence and decides what should be on screen. Without it
**the app will not run** — it stops with an error.

> ⚠️ **Your Gemini key must have BILLING TURNED ON.** This is the single most common
> reason people say "it doesn't work". On the free tier the quota runs out after a few
> scenes → the app can't pick visuals → **your video comes out random and wrong**.
>
> - Turn on billing at **https://aistudio.google.com/app/apikey** (or Google Cloud Console).
>   It's pay-as-you-go and costs **a few cents per video**. You just need billing *enabled*
>   so the quota isn't tiny.
> - 🚫 **A Google One / Gemini Advanced subscription does NOTHING here.** That's a consumer
>   plan. You need **API billing**. They are completely separate things.

### 👤 The Presenter — optional

A recurring person who appears on camera now and then. Made once, reused forever.
Needs a **HeyGen** key. **Skip this entirely** if you want a faceless video — everything
else works without it.

---

## 3. What you need on your computer

- A **Mac** or **Windows** (10/11).
- **Node.js** — the app's engine. Get the **LTS** button at **https://nodejs.org/**, install (Next → Next).
- **FFmpeg** — the tool that glues the video together.
  - **Windows** (easiest): download **ffmpeg-release-essentials.zip** from
    **https://www.gyan.dev/ffmpeg/builds/**, unzip it, and **copy its `bin` folder into
    the app folder** (the folder with `install.bat` in it). The app finds it by itself —
    nothing to configure.
  - **Mac**: open the **Terminal** app and type: `brew install ffmpeg`
    (no `brew`? install Homebrew first from **https://brew.sh/**).

---

## 4. Install it (once)

1. **Unzip the app.** Your coach sends it as a ZIP. Put the folder anywhere (e.g. Documents).
2. **Windows**: double-click **`install.bat`** · **Mac**: double-click **`install.command`**.
3. A black window opens, downloads for a minute or two, says **"Done!"**.

> ⚠️ **Mac — «"install.command" is damaged and can't be opened»?**
> The file is **fine**. macOS blocks anything that arrived from the internet. Fix it once:
> 1. Open **Terminal** (Spotlight 🔍 → type "Terminal" → Enter).
> 2. Type `xattr -cr ` — **with a space at the end**. Don't press Enter yet.
> 3. **Drag the app folder** from Finder into the Terminal window. Its path appears by itself.
> 4. Press **Enter**. Done, permanently.
> 5. Double-click `install.command` again — it opens normally.

---

## 5. Start it (every time)

- **Windows**: double-click **`start.bat`** · **Mac**: double-click **`start.command`**.

A black window opens and stays open. **That window is the engine — don't close it while
you work.** Your browser opens at **http://localhost:3000**.

To stop: close that black window (or use `stop.bat` / `stop.command`).

---

## 6. Put in your keys (the **Settings** page)

Click **Settings**, top right. Paste only the keys for the jobs you chose in §2:

- **Google Gemini** — required (billing on! see §2).
- **Your voice provider's key** — then pick the voice itself.
- **kie.ai** — for AI pictures.
- **Pexels / Pixabay** — for real footage (optional, but strongly recommended).
- **HeyGen** — only if you want a presenter, **or** if you're using HeyGen as your voice.

Click **Save**.

> 🔒 Your keys stay **on your computer**, in a local file. A saved key shows as dots (•••).
> If you don't touch that field, it won't change.

There's also a **full settings** page (link at the bottom) with every knob in the app.
You don't need it to make videos.

---

## 7. Make your first video

Go to **Create a video**:

1. **Title** *(optional)* — so you can find it later.
2. **Channel** *(optional)* — a saved preset, see §8. Or "None — manual settings".
3. **Script** — paste your full narration.
4. **Avatar** — pick a ready presenter, or **None** for a faceless video.
5. **Visual mode** — `Real footage`, `AI images`, or `Mix` (both).
6. **Real / AI balance** (in Mix) — e.g. 80% real / 20% AI.
7. **Seconds per visual** — how long each shot stays on screen (4–6s is normal).
8. **Avatar on screen (%)** — how often the presenter appears. 15–25% is plenty.
9. **Create the video.**

You land on the tracking page and watch it work, step by step.

---

## 8. Presenters and Channels (both optional)

**Avatars page** — make a presenter once:
- Give it a **name**.
- Either **upload a photo** (sharp, front-facing, well-lit) **or** describe the person in
  words and let the app draw them.
- **Avatar quality**: there are two engines. The higher-quality one looks better but
  costs roughly **3× more per minute** (see §11). Your choice — it is not free.
- Wait for **Ready** ✅.

**Channels page** — save a preset so you don't re-configure every time:
- Name, visual mode, AI style, seconds per visual, format (`1920x1080` normal / `1080x1920`
  Shorts), voice speed, and a **visual prompt** that steers *what* gets shown.
- Example visual prompt: *"Historical documentary. For each line, give a 3–8 word visual
  query of concrete nouns: places, objects, real archive footage. Avoid the abstract."*

---

## 9. ⚠️ About YouTube footage — read this

**YouTube is switched ON by default**, and it sits **first** in the list of sources.

**There is no copyright filter.** The app does **not** check licences and does **not**
limit itself to Creative-Commons clips. It picks whatever fits your scene best.

> **You are responsible for what you publish.** If you don't want that risk, turn YouTube
> off: **full settings → `YT_DLP_ENABLED` → `0` → Save.** Everything still works — the
> app just uses Pexels/Pixabay/Wikimedia/AI instead.

*(If you previously read that this was "off by default" or "Creative Commons only" —
that was wrong, and this guide is the correction.)*

---

## 10. While it's running — the two rules

### 🛑 Rule 1: don't let your computer go to sleep

This is the **number one** cause of a ruined run. A dark screen is fine — a **sleeping
computer** is not. They're two different settings:

| | Result |
|---|---|
| **Screen turns off** | ✅ fine, the video keeps building |
| **Computer goes to sleep** | ❌ everything stops |

**Windows**: Settings → System → **Power & battery** → **Screen and sleep** →
**"Sleep: put my device to sleep after" → Never**. On a laptop set **both** columns
(battery + plugged in), and keep it plugged in.
**Also: don't close the lid** — that sleeps it. (Power → "Choose what closing the lid does" → **Do nothing**.)

**Mac**: System Settings → **Lock Screen / Battery** → set the computer to never sleep
while plugged in.

### ⏱️ Rule 2: know how long it really takes

Be realistic — this is not instant:

| Video | Roughly |
|---|---|
| A few minutes long | several minutes |
| 10–20 minutes long | tens of minutes to a couple of hours |
| **1 hour+ (hundreds of scenes)** | **many hours — plan for half a day** |

Very long videos are genuinely heavy. If you can, **split them into parts** — it's far
more reliable than one giant run.

---

## 11. If a run stops or breaks — **Resume it, don't restart**

If a run is interrupted (sleep, a crash, you stopped it, the black window closed), you
**do not** have to start over and pay again.

1. Open the run (from **Jobs**).
2. If it still says *running* but nothing is happening, click **Stop**.
3. A **Resume run** button appears → click it.
4. It picks up where it left off and **reuses everything already generated** — you are
   not charged twice for finished scenes.

> ✅ Resume needs the narration and the scene plan to already exist. If the run died in
> the first few seconds (before those were made), there's nothing to resume — just start
> a new one; nothing was lost.

> 🗑️ **Careful with Delete.** Deleting a job **permanently erases its files from your
> disk** — the finished video and every generated scene. It cannot be undone. If a run is
> merely stuck, use **Stop → Resume** instead. (Your spending history is kept on the
> **Costs** page either way.)

---

## 12. What it costs

The app is free. You pay only the services you chose in §2. The **Costs** page tracks
what each video actually spent.

| Service | Roughly |
|---|---|
| **Gemini** (the Brain) | a few cents per video |
| **ElevenLabs** (if used) | ~$0.22 per 1,000 characters |
| **HeyGen presenter** | ~**$3/min** high quality · ~**$1/min** standard — and only for the ~15% of scenes where they appear |
| **kie.ai** images | ~$0.02 per image |
| **kie.ai** Veo video | ~$0.40 per **second** — expensive, off by default |
| **Pexels · Pixabay · Wikimedia · Openverse · Archive** | **free** |

> ⚠️ **These are the app's own estimates, not official price lists.** Providers change
> pricing; always check your own dashboard for what you're actually being billed.

**To spend less:** use **Real footage** mode, keep the presenter low (or none), keep AI on
**images** rather than video, and use the **standard** avatar quality.

---

## 13. When something goes wrong

| What you see | What it means / what to do |
|---|---|
| **Mac: "…is damaged and can't be opened"** | Not damaged — macOS blocks internet downloads. Fix once with `xattr -cr` (see §4). |
| **Footage is random / off-topic; video came out bad** | Your **Gemini** key is on the free tier and hit its quota. **Turn on API billing** (§2). This is the #1 cause. Not Google One — API billing. |
| **The run just stopped, no error** | Almost always the computer went to sleep (§10). **Stop → Resume** (§11). |
| **"FFmpeg failed" / no final video** | FFmpeg isn't found. **Windows**: copy ffmpeg's `bin` folder into the app folder. **Mac**: `brew install ffmpeg`, then restart the app. |
| **Avatar stuck on "Preparing" / "Error"** | Check the **HeyGen** key. A blurry or rejected photo fails — try another. |
| **No voice / voice error** | The key for your chosen voice provider is missing, or no voice is selected. |
| **kie.ai "402" / "401"** | **402** = out of credits, top up. **401** = wrong key. |
| **No real footage found** | Add a **Pexels** and/or **Pixabay** key. Without them you'll mostly get AI. |
| **The black window closed** | That was the engine. Relaunch `start.bat` / `start.command`, then **Resume** the run (§11). |
| **I want vertical / Shorts** | Make a channel with **Format = 1080x1920** and use it. |

---

## 14. Where your stuff lives

- **Keys, presenters, history, videos**: in a hidden folder in your user profile —
  `C:\Users\YOU\.faceless-studio` (Windows) or `~/.faceless-studio` (Mac).
- **An app update never touches it.** Your keys and videos survive updates.
- Finished videos: in that folder under `runs/<name>/final.mp4` — or just click **⬇ mp4**
  on the **Jobs** page.

---

## 15. Updating

Your coach sends a new ZIP. Your keys, presenters and videos are kept (they live outside
the app folder — see §14). Steps: **[UPDATE.md](./UPDATE.md)**.

---

## The 60-second recap

1. Install **Node.js** + **FFmpeg** — once.
2. Unzip the app → `install` → `start`.
3. **Settings** → **Gemini (billing ON!)** + your **voice** key + **kie.ai** → Save.
   Add **Pexels/Pixabay** for real footage. **HeyGen** only if you want a presenter.
4. *(optional)* **Avatars** → make a presenter. **Channels** → save a preset.
5. **Create a video** → paste script → **Create**.
6. **Don't let the computer sleep.** If it stops → **Stop → Resume**, never restart from zero.
7. **Jobs** → **⬇ mp4**.

Happy filming 🎬
