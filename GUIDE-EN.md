# Faceless Video Generator — the complete guide

> **For everyone. No technical skills needed.**
> You paste a script. The app builds a finished YouTube video — narration, visuals,
> and (optionally) a presenter who both talks on camera *and* appears inside the shots.
> Everything runs **on your own computer**.
>
> 💳 **Paying for the services — read before your first video:** [BILLING.md](./BILLING.md)
> 🔄 **Already installed — how to update:** [UPDATE.md](./UPDATE.md)
> 🇫🇷 Version française : [GUIDE-FR.md](./GUIDE-FR.md)

---

## 1. What actually happens (in 30 seconds)

```
        Your script (plain text)
                 │
                 ▼
   1. A VOICE reads it out loud                    → the narration
                 │
                 ▼
   2. The app cuts the narration into short "shots"
      (a few seconds each, following the voice's own timing)
                 │
                 ▼
   3. For every shot, it finds something to show
      • real footage or photos from the internet, and/or
      • an AI-generated image or video clip
      • now and then → your PRESENTER talks on camera (optional)
      • and, if you want it → the presenter appears INSIDE an ordinary shot
                 │
                 ▼
   4. Everything is glued into one MP4, ready to upload
```

You can also **skip step 1** and upload narration you recorded yourself.

---

## 2. The jobs — and you choose who does each

This is the most important page in this guide. **The app is not locked to any one company.**
A video needs a few jobs done, and for each one you pick who does it:

| # | The job | What it means | Do I need it? |
|---|---|---|---|
| 🎙️ | **The Voice** | reads your script out loud | **Yes** — pick one (or upload your own audio) |
| 🖼️ | **The Pictures** | what's on screen while the voice talks | **Yes** — pick at least one |
| 🧠 | **The Brain** | decides *what to show* for each sentence | **Effectively yes** — see the warning below |
| 👤 | **The Presenter** | a person on camera, now and then | **No** — optional |
| ⏱️ | **The Timer** | finds where each word falls in *uploaded* audio | only if you **upload** narration |

You only pay for the ones you use. **You do not need every key in this guide.**

### 🎙️ The Voice — pick ONE

**Settings → Voice provider.** The page then shows that provider's key field and its voice
field, and nothing else — you never need the other providers' keys.

| Option | You need | Notes |
|---|---|---|
| **ElevenLabs (direct)** | an ElevenLabs key | **the default** — best known, huge voice library. **Load voices** picker. |
| **GenAIPro** | a GenAIPro key | an ElevenLabs reseller — same voices, different billing |
| **AI84** | an AI84 key | resells **ElevenLabs *and* MiniMax** through one key. **Load voices** picker. The *model* you pick decides which engine you're on — cloned voices exist only on the MiniMax side. |
| **ai33.pro / OpenSpeaker** | an ai33 key | fronts **six** engines (clone / ElevenLabs / MiniMax / Fish Audio / Edge / Vbee). The engine travels inside the voice id, so there's nothing extra to set. **Load voices** picker. |
| **Fish Audio** | a Fish Audio key | **Load voices** picker |
| **Hume AI (Octave)** | a Hume key | **Load voices** picker; the picker flags voices that need `HUME_VERSION = 2` |
| **69labs** | a 69labs key | ElevenLabs / EdgeTTS / voice cloning through one gateway |
| **HeyGen** | a HeyGen key | convenient if you already use HeyGen for the presenter. **Load voices** picker. |
| **MiniMax** | a MiniMax key **+ Group ID** | cheap, good quality, supports cloning. **Both fields are required.** |

> 🎙 **Or supply your own narration.** On the Create page choose **Upload voiceover** instead
> of **Script** and drop in an mp3/wav/m4a/aac/flac/ogg (up to **50 minutes**). Then you need
> no voice provider at all — but you **do** need a **Groq** key (see The Timer below).

### 🖼️ The Pictures

**Real footage** — *Settings → Advanced → Real footage sources.* All ten ship switched **on**:

| Source | Key needed? | What you get |
|---|---|---|
| **Pexels** | free key | the workhorse — good stock video **and** photos. You can add **several keys**; the app rotates them to raise the rate limit. |
| **Storyblocks (paid)** | a paid **key pair** (public + private) | professionally shot stock video. The only paid source here. |
| **Pixabay** | free key | more stock video + photos |
| **Openverse** | **no key** | freely-licensed photos |
| **Wikimedia** | **no key** | historical / archive photos |
| **Archive.org** | **no key** | old archive footage |
| **Web (Google)** | 2 keys (`GOOGLE_CSE_KEY` + the search-engine id `cx`) | open-web image search. Leave the keys empty and this source is simply inert. |
| **YouTube (clips)** | no key, but ⚠️ **see §9** | real clips from YouTube |
| **Wigolo (web photos)** | **no key, no signup** | open-web **photos**, served by a small helper the app starts for itself. Free. |
| **Brave** | `BRAVE_API_KEY` | open-web photos, plus video results that come down through yt-dlp. **The only footage source that bills per search** — about $5 per 1000, so roughly $0.17 a video. Wigolo does the same job for free; use Brave only if the free sources are not enough. |

**AI-generated pictures** — *Settings → AI provider (images / video).* Pick **one**:

| Option | You need | Notes |
|---|---|---|
| **kie.ai (nano-banana / Veo)** | a kie.ai key | **the default.** Prepaid credits, no subscription. |
| **69labs (Grok)** | a 69labs key | the widest catalogue here — 13 image models, 4 video models |
| **Magnific AI (Mystic / Hailuo)** | a Magnific key | subscription only; **the free plan has no API access** |
| **Runware** | a Runware key | marked *Experimental*. One API spanning a ~100× price range, so you pick your own quality/price point. |
| **Higgsfield (Soul / DoP)** | a key **+ secret** | Soul images, DoP cinematic video |

> 💡 **You'll usually want both kinds**: real footage first, AI as the backup for shots where
> nothing real fits. That's what **Mix** mode does, and it is the default.

### 🧠 The Brain — Google Gemini

Gemini reads each sentence and decides what should be on screen for it.

> ⚠️ **This is the single most important key in the app, and the way it fails is the trap.**
> Without a Gemini key the app **does not stop with an error** — it quietly falls back to
> searching your sentence word-for-word, and the footage comes out literal and off-topic. In
> the run log you'll see `GOOGLE_API_KEY not set — using beat text as the visual query`.
>
> **And the key's API billing must be turned on.** On the free tier the quota runs out after
> a few shots and the rest of the video degrades exactly the same way. This is by far the most
> common cause of "the video came out bad".
>
> - Get the key and enable billing at **https://aistudio.google.com/app/apikey**.
>   Pay-as-you-go, a few cents per video.
> - 🚫 **A Google One / Gemini Advanced subscription does NOTHING here.** That's a consumer
>   plan. You need **API** billing. They are completely separate things.

### 👤 The Presenter — optional

A recurring person, made once from one photo and reused forever. Needs a **HeyGen** key.
**Skip it entirely for a faceless video** — everything else works without it.

On this build the presenter can do **two** things (see §7 and §8):

- **talk on camera** — HeyGen animates him, lip-synced to your narration;
- **appear inside ordinary shots** ("cameos") — the same man, doing what the line describes,
  drawn from his reference photo. That one is generated by your AI image provider, not HeyGen.

### ⏱️ The Timer — Groq, only for uploaded narration

If you upload your own audio, the app has no script timing to work from, so **Groq Whisper**
transcribes it and reports where every word falls. **Required** for *Upload voiceover* —
the app refuses the run up front if the key is missing, before anything is spent.

It has a generous free tier and most people never pay for it. It also sharpens the timing of
*synthesized* narration on every provider except ElevenLabs (which reports its own timings).

---

## 3. What you need on your computer

- A **Mac** or **Windows** (10/11).
- **Node.js 20 or newer** — the app's engine. Take the **LTS** button at
  **https://nodejs.org/** and click through the installer.
- **FFmpeg** — the tool that glues the video together.
  - **Windows** (easiest): download **ffmpeg-release-essentials.zip** from
    **https://www.gyan.dev/ffmpeg/builds/**, unzip it, and **copy its `bin` folder into
    `C:\Users\YOU\.faceless-studio\bin`** (create the `bin` folder if it isn't there; the
    `.faceless-studio` folder appears after the first start, or make it yourself). The app
    looks there by itself — nothing to configure, no PATH editing — and, unlike the app
    folder, that place **survives every update**.
  - **Mac**: open **Terminal** and run `brew install ffmpeg`
    (no `brew`? install Homebrew first from **https://brew.sh/**).
    The app also checks `/opt/homebrew/bin` and `/usr/local/bin` directly, so FFmpeg is found
    even when the launcher doesn't inherit your Terminal's settings.

---

## 4. Install it (once)

1. **Unzip the app.** Your coach sends it as a ZIP. Put the folder anywhere (e.g. Documents).
2. **Windows**: double-click **`install.bat`** · **Mac**: double-click **`install.command`**.
3. A black window opens, downloads for a minute or two, and says **"Done!"**.

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

A black window opens and stays open. **That window is the engine — don't close it while you
work.** Your browser opens at **http://localhost:3001**.

To stop: close that black window (or use `stop.bat` / `stop.command`).

The top of the app has six pages: **Create a video · Avatars · Channels · Jobs · Costs ·
Settings**.

---

## 6. Put in your keys (the **Settings** page)

> 💳 **Before this step, read [BILLING.md](./BILLING.md).** It covers how each service actually
> charges — which need money added before they'll work at all, which are free, and the biggest
> trap of all: **a normal subscription usually does NOT include API access** (HeyGen
> especially). That one page prevents most "it doesn't work" situations.

The page opens as **six one-line rows** — one per step, in the order the pipeline uses them,
each showing its own answer on the right ("69labs", "Magnific AI", "Images + Videos"). Click a
row to open it. It shows **only what your choices need**: pick a provider and its key field and
its models appear underneath, and the others never clutter the page.

**Almost nothing here has to be submitted.**

- A control whose value is **complete the moment you click it** — a checkbox, one of the
  bordered choice cards, a dropdown — **writes itself immediately.** Ticking a footage source
  or changing a provider is already saved; there is nothing to press afterwards and nothing to
  lose by navigating away.
- **Every API-key row has its own Save, right beside the box you pasted into.** It writes *only*
  that key, so a half-typed key in another row is left exactly as it was.
- The **Save** on the title row is for the remaining typed fields — speeds, counts, a voice ID.
  It stays greyed out until one of them changes, and says how many changes are waiting.

Working down the six rows:

| Row | Fill in |
|---|---|
| **1 · Voice** | the voice provider → its API key and voice field appear below (most have a **Load voices** button) · **voiceover speed** (`0.7` slow → `1.2` fast; `0.93` is shipped, a channel can override it) · **Groq — API key**, required for *Upload voiceover* and recommended on any non-ElevenLabs voice |
| **2 · Avatar** | **HeyGen — API key**. Only if you want a presenter. |
| **3 · AI visuals** | the AI provider → its image / video models and its API key appear below · **presenter in the shots**: the model that keeps his face, and the one key that lets his shots *move* (the page asks for exactly one, and says which) |
| **4 · Real footage** | **Pexels — API keys** (free; add several and the app rotates them) · **Pixabay** · **Storyblocks**, paid and a **pair**: public + private · **Brave**, paid · the two **Google** web-search keys, paid · **Google Gemini — API key** ⚠️ **billing must be enabled** (§2) · and the ten **real footage source** checkboxes |
| **5 · AI Fallback Media** | what may be generated when a real shot finds nothing — **Images only** is the shipped default and the cheap one |
| **6 · Advanced (optional)** | seconds per visual · default AI image style · a link to **full settings** |

> 🔒 Your keys stay **on your computer**, in a local database. A saved key is shown as a mask
> **beside its name** — `sk_V••••••DaIg` — and the input below it is **empty**: that empty box
> is where you paste a *replacement*. Leave it alone and the stored key is untouched. The app
> never writes a mask back over a real key, and it never prints a key on screen in full.

**full settings** (linked at the bottom of Advanced) has every knob in the app. You don't need
it to make videos; §9 and §12 point at the two switches that are actually worth knowing.

---

## 7. Make your first video

Go to **Create a video**:

1. **Title** *(optional)* — so you can find it later.
2. **Channel** *(optional)* — a saved preset, see §8. Or "None — manual settings".
3. **Narration source**:
   - **✍ Script → voiceover** — paste your script; we generate the narration. The word count
     and an estimated length appear under the box.
   - **🎙 Upload voiceover** — drop in your own recording (mp3, wav, m4a, aac, flac, ogg; up to
     **50 minutes**). Needs the **Groq** key; the page says so, with a link, if it's missing.
4. **Avatar** — pick a ready presenter, or **None** for a faceless video.
5. **The presenter appears IN the shots** *(only once an avatar is picked)* — two example
   tiles show the difference. Switch it on and you get:
   - **How many shots contain him** — a percentage (0–60, ships at 35).
   - **Does he move in those shots** — **Photo with a slow zoom** (cheaper, usually enough) or
     **Moving clip** (he actually performs the action; adds around two minutes of render per
     shot, and needs a **kie.ai**, **Magnific** *or* **Higgsfield** key).
6. **Video settings**:
   - **Visual mode** — **Full AI** / **Real footage** / **Mix**, with an example of each.
   - **Look of the generated shots** — three tiles, all showing the *same scene* so the
     difference is the look and nothing else. One carries a **from Settings** badge: that's
     the one your Settings page holds, and leaving it selected means "whatever Settings says".
     - **Ultra-real (default)** — the look of channels like Elias Yoder and Frank Miller: a
       frame grabbed from a real handheld video, not a polished render. **The least
       AI-looking option**, and the counter-intuitive one — asking for *less* polish is what
       stops footage reading as stock. It is what most people here are aiming for, which is
       why it is the one you get without choosing.
     - **Cinematic (polished)** — polished documentary: sharp, well-lit, high production value.
     - **Black & white documentary** — a deliberate darkroom print, not colour with the colour
       removed.
   - **AI media** *(Full AI and Mix)* — **Images only** (cheapest) / **Auto** / **Video only**.
   - **AI photo / video balance** — appears only on **Auto**; sets how much of the AI half is
     moving video.
   - **Real footage media** *(Real and Mix)* — photos only / photos + videos / videos only.
   - **Fallback behaviour** — **Allow AI fallback (recommended)**, or **Real footage only**
     if you would rather a shot be dropped than generated.
   - **Real / AI balance** *(Mix)* — e.g. 80% real / 20% AI.
   - **Seconds per visual** — the *target* length of a shot. 4–6s is normal.
   - **One visual stays on screen** — the shortest and longest a shot may run, e.g. `3–10s`.
     **The maximum is the one that matters.** The setting above is only a target: a shot is
     never cut in the middle of a sentence, so a long sentence holds the picture right up to
     this ceiling. Setting the target to 3s while the ceiling sits at 10s still gives you
     nine-second shots — that is the single most common surprise on this page.
     - Above **~10s**, a generated *video* shot replays from its beginning, because real AI
       clips are only 5–8 seconds long, and the restart is visible. Photos have no such
       limit: the slow zoom stretches to any length.
     - Below **~4s**, some shots get cut mid-sentence. That is the trade — a fast rhythm
       against cuts that land awkwardly.
   - **Avatar on screen** — how often the presenter *talks on camera*. 15–25% is plenty.
   - **Scene transitions (dip to black)** and **Informational overlays** — two optional
     finishing touches.
7. **Create the video.**

You land on the run page and watch it work, step by step, with a live log.

> 🛡️ **Before anything is charged, the page checks your keys.** If the voice or AI provider
> you picked has no key, a red box above the button lists exactly what is missing (with a
> link to Settings) and the button stays off. A yellow box means the video will run but
> worse — for example no Gemini key. Nothing is started, nothing is billed, until the red
> list is empty.

---

## 8. Presenters and Channels (both optional)

### Avatars page — make a presenter once

- Give it a **name**.
- Pick the **Avatar engine** — this is a real cost decision, made once per avatar:

  | Engine | Cost | Notes |
  |---|---|---|
  | **Avatar IV** *(recommended)* | ~**$3/min** | highest realism |
  | **Legacy** | ~**$1/min** | slightly less realistic, three times cheaper |
  | **Avatar V** | *estimated* **$4/min** | highest quality, but only for HeyGen avatars that already support it — the app lists yours and lets you pick |

  The minutes counted are only the ones the presenter is actually on screen.
- Then **one** of three:
  - **upload a photo** — sharp, front-facing, well-lit. **16:9 landscape, at least 1920px wide**
    gives the best result; a small or oddly-shaped photo is upscaled and shows.
  - **describe the person in words** and let the app draw them, or
  - **paste the ID of an avatar you already made on HeyGen**.
- Wait for **Ready** ✅. If it sticks on *Preparing* or *Error*, the **Logs** button on the
  card says why.

> 📸 **The reference photo matters more than it used to.** Cameo shots are generated at very
> high resolution, so a soft avatar now cuts against a razor-sharp shot of the same man.

### Channels page — save a preset

On this build a channel stores **a name, a default avatar, a voice, and a voice speed**. Pick
it on the Create page and those apply without retyping. Everything else — mode, look, pacing,
percentages — is chosen per video on the Create page.

> 📐 **Vertical / Shorts:** the frame size is not on the Channels form in this build. Set it in
> **full settings → `VIDEO_RESOLUTION` → `1080x1920` → Save**, and change it back for normal
> videos.

---

## 9. ⚠️ About YouTube footage — read this

**YouTube is switched ON by default**, and it sits **first** in the list of sources.

**There is no copyright filter.** The app does **not** check licences and does **not** limit
itself to Creative-Commons clips. It picks whatever fits your shot best.

> **You are responsible for what you publish.** To turn it off:
> **Settings → Real footage → untick "YouTube"** (the checkbox saves itself — there is no
> Save to press).
> Everything still works — the app just uses the other sources instead.

Two of the other sources are worth a sentence for the same reason:

- **Wigolo**, **Web (Google)** and **Brave** are **open-web** photos, so they are not
  licence-filtered either. The app does strip results from stock agencies and re-upload sites, and refuses any
  frame carrying a visible watermark — but the licence question is still yours.
- **Pexels · Pixabay · Openverse · Wikimedia · Archive.org** are free for commercial use, and
  **Storyblocks** is properly licensed because you pay for it. Those six are the safe set: if
  publishing risk matters more to you than variety, leave only those ticked.

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

**Mac**: System Settings → **Lock Screen / Battery** → set the computer never to sleep while
plugged in.

### ⏱️ Rule 2: know how long it really takes

| Video | Roughly |
|---|---|
| A few minutes long | several minutes |
| 10–20 minutes long | tens of minutes to a couple of hours |
| **1 hour+ (hundreds of shots)** | **many hours — plan for half a day** |

Very long videos are genuinely heavy. If you can, **split them into parts** — far more
reliable than one giant run. Turning on **Moving clip** cameos or **AI video** adds a lot of
wall-clock time as well as money.

---

## 11. If a run stops or breaks — **Resume it, don't restart**

If a run is interrupted (sleep, a crash, you stopped it, the black window closed), you **do
not** have to start over and pay again.

1. Open the run (from **Jobs**).
2. If it still says *running* but nothing is happening, click **Stop**.
3. A **Resume run** banner appears → click **Resume run**.
4. It picks up where it left off and **reuses everything already generated** — you are not
   charged twice for finished shots.

> ✅ Resume needs the narration and the shot plan to already exist. If the run died in the
> first few seconds, there is nothing to resume — just start a new one; nothing was lost.

> 🗑️ **Careful with Delete.** Deleting a job **permanently erases its files from your disk** —
> the finished video and every generated shot. It cannot be undone. If a run is merely stuck,
> use **Stop → Resume**. (Your spending history stays on the **Costs** page either way.)

---

## 12. What it costs

The app is free. You pay only the services you chose in §2. The **Costs** page tracks what
each video actually spent, in US dollars.

These are the app's own default rates, which is what the Costs page uses until you overwrite
them with what your invoice actually says:

| Service | Rate the app assumes |
|---|---|
| **Gemini** (the Brain) | a few cents per video |
| **ElevenLabs** (if used) | **$0.22** per 1,000 characters |
| **HeyGen presenter** | **$3/min** Avatar IV · **$1/min** Legacy · **$4/min** Avatar V *(estimated)* — and only for the shots where he actually talks |
| **kie.ai image** (the default AI picture, Nano Banana Pro) | **$0.09** each — the cheaper Nano Banana ($0.02) is one click away in Settings → AI visuals |
| **kie.ai Veo Fast video** | **$0.325** per **clip** — *not* per second |
| **Magnific image / video** | $0.119 per image · $0.35 per clip |
| **Groq** (uploaded narration) | $0.111 per hour of audio — fractions of a cent |
| **Pexels · Pixabay · Wikimedia · Openverse · Archive · Wigolo** | **free** |
| **Brave** | ~$5 per 1000 searches (~$0.17 a video) — the only real-footage source that bills |
| **Storyblocks** | whatever your plan costs |

> ⚠️ **These are estimates, not invoices.** Some providers report what they actually charged
> and the page uses that instead; where nobody has a figure the page says **"rate not set"**
> rather than showing a confident $0.00. Your own dashboard is always the truth.

> 🔎 **Costs → "Check accounts"** asks the providers that expose a balance — kie.ai, HeyGen, 69labs and Magnific — whether they still have credit; the others have no such endpoint, so check them on their own dashboards.
> It is free and generates nothing. Worth doing when videos suddenly look worse for no reason:
> a provider that has run dry doesn't announce itself — the app just quietly falls through to
> the next one.

**To spend less:** use **Real footage** or **Mix**, keep the presenter percentage low (or use
no avatar), keep **AI media** on **Images only**, keep cameos on **Photo with a slow zoom**,
and pick the **Legacy** avatar engine.

---

## 13. When something goes wrong

| What you see | What it means / what to do |
|---|---|
| **Mac: "…is damaged and can't be opened"** | Not damaged — macOS blocks internet downloads. Fix once with `xattr -cr` (§4). |
| **Footage is random / off-topic; the video came out bad** | The **Gemini** key is missing, or it's on the free tier and hit its quota. **Add the key and turn on API billing** (§2). This is the #1 cause. Not Google One — API billing. |
| **The run just stopped, no error** | Almost always the computer went to sleep (§10). **Stop → Resume** (§11). |
| **"FFmpeg failed" / no final video** | FFmpeg isn't found. **Windows**: copy ffmpeg's `bin` folder into `C:\Users\YOU\.faceless-studio\bin` (§3). **Mac**: `brew install ffmpeg`, then restart the app. |
| **"FFprobe was not found"** | Same thing — you have ffmpeg but not ffprobe. They're two separate downloads; install both. |
| **Avatar stuck on "Preparing" / "Error"** | Check the **HeyGen** key, then the **Logs** button on the avatar card. A blurry or rejected photo fails — try another. |
| **The presenter is missing from the finished video** | Almost always an empty HeyGen **API wallet** — not the subscription (see BILLING §5). The run page marks such a video as *degraded* rather than pretending it succeeded. |
| **The presenter's cameos didn't appear** | Cameos need an AI image provider that can hold a face and a reference photo still on disk. The run log ends with a line saying how many of them rendered with him. |
| **No voice / voice error** | The key for your chosen voice provider is missing, or no voice is selected. The app refuses the run before spending anything. |
| **"Uploading a voiceover requires a Groq API key"** | Exactly that — add `GROQ_API_KEY` in Settings, or paste a script instead. |
| **kie.ai "402" / "401"** | **402** = out of credits, top up. **401** = wrong key. |
| **A provider seems to do nothing** | **Costs → Check accounts.** An account that has run dry looks identical to one that simply found nothing. |
| **"The video was not made" box on the run page** | The app names the provider that stopped the run and what to do (empty wallet, rejected key, plan lapsed…). Fix that one thing, then **Resume** or create the video again. The raw error is still in the log below it. |
| **"Completed with warnings" on a finished run** | The video exists but is not what you asked for — the box says what fell short (no presenter, black beats, cut-off narration, Gemini unavailable…). Read it before publishing. |
| **Jobs shows "file missing" instead of mp4** | The run finished, but its file is no longer where this install keeps videos — it was moved or deleted, or the data folder changed. The history stays; the video does not. |
| **No real footage found** | Add **Pexels** and/or **Pixabay** keys. Without them you'll mostly get AI. |
| **Shots stay on screen far longer than the seconds you set** | The seconds box is a *target*, not a limit. Lower the **maximum** in **One visual stays on screen** — a shot is never cut mid-sentence, so a long sentence rides up to that ceiling whatever the target says. |
| **Generated shots look nothing like the look you picked** | Something in **Settings → AI image style** is fighting the look profile. The Create page shows a warning naming the conflicting words, with a link to fix it. |
| **The black window closed** | That was the engine. Relaunch `start.bat` / `start.command`, then **Resume** the run (§11). |
| **I want vertical / Shorts** | **full settings → `VIDEO_RESOLUTION` → `1080x1920`** (§8). |

---

## 14. Where your stuff lives

- **Keys, presenters, history, videos**: in a hidden folder in your user profile —
  `C:\Users\YOU\.faceless-studio` (Windows) or `~/.faceless-studio` (Mac).
- **An app update never touches it.** Your keys and videos survive updates.
- Finished videos: in that folder under `runs/<name>/final.mp4` — or just click **⬇ mp4** on
  the **Jobs** page.

---

## 15. Updating

Your coach sends a new ZIP. Your keys, presenters and videos are kept (they live outside the
app folder — see §14). Steps: **[UPDATE.md](./UPDATE.md)**.

---

## The 60-second recap

1. Install **Node.js 20+** and **FFmpeg** — once.
2. Unzip the app → `install` → `start`.
3. **Settings** → **Gemini (billing ON!)** + your **voice** provider's key + your **AI
   provider's** key — each row has its own **Save** next to the box. Add **Pexels** (and
   Pixabay) for real footage. **HeyGen** only if you want a presenter. **Groq** only if you
   upload your own narration.
4. *(optional)* **Avatars** → make a presenter. **Channels** → save a preset.
5. **Create a video** → paste the script → pick the mode and the look → **Create**.
6. **Don't let the computer sleep.** If it stops → **Stop → Resume**, never restart from zero.
7. **Jobs** → **⬇ mp4**.

Happy filming 🎬
