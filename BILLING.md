# Paying for the services — what to set up, and in what order

> **Read this before your first video.** Almost every "it doesn't work" message we get
> turns out to be a billing setup that was never finished. The app itself is free; you
> pay the AI services directly, and **most of them bill their API separately from their
> normal subscription.** That surprise is the single most common blocker.

---

## The one rule that catches everyone

> **A normal subscription on a service's website does NOT automatically give you API access.**

Several of these companies run two separate wallets: one for using their website, and one
for programs (like this app) talking to them. Paying for the first does nothing for the
second. **HeyGen works exactly this way** — this is the #1 thing people get stuck on.

Each section below tells you which model that service uses.

---

## Three ways these services charge

| Model | What it means | Who does it |
|---|---|---|
| 💳 **Prepaid** | You deposit money; usage draws it down; at zero it just stops | Gemini · kie.ai · HeyGen API |
| 📅 **Subscription** | Monthly plan with an included allowance; API draws from the same pool | ElevenLabs |
| 🆓 **Free** | Just a key, no payment ever | Pexels · Pixabay · Wikimedia · Openverse · Archive.org |

**Prepaid is your friend.** You cannot overspend — when the balance hits zero, generation
stops. Don't turn on auto-reload until you know your monthly volume.

---

## 1. 🧠 Google Gemini — **REQUIRED, nothing works without it**

Gemini decides what to show on screen for each sentence. Without it the app stops with an
error; with it on the *free* tier your footage comes out random and off-topic — this is by
far the most common cause of "the video came out bad".

| | |
|---|---|
| **Billing model** | 💳 Prepaid deposit (now the default for new accounts) |
| **Minimum** | **$10** |
| **Free tier** | Exists, but the quota is far too small for a real video |
| **Get the key** | https://aistudio.google.com/app/apikey |
| **Add money** | Same place — billing is managed inside AI Studio |
| **What it costs you** | A few cents to a couple of dollars per video |

> ⚠️ **A Google One / Gemini Advanced subscription does NOT count.** That's a consumer plan
> and does nothing for the API. You need **API billing** specifically. People lose days to this.

**Do this:** create the key → enable billing → deposit $10 → paste the key into Settings.
Leave auto-reload OFF at first.

---

## 2. 🎙️ The voice — pick ONE provider

The app supports several. **You only need a key for the one you choose** in
**Settings → Voice provider**.

### ElevenLabs — the default, best-known

| | |
|---|---|
| **Billing model** | 📅 Subscription. **The API and the website share ONE credit pool** — there is no separate API balance |
| **Free tier** | 10,000 credits/month, and the API does work on it — **but free-tier output cannot be used commercially** |
| **For commercial use** | Any paid plan: Starter **$6/mo** (30k credits) · Creator **$22/mo** (121k) · Pro **$99/mo** (600k) |
| **Get the key** | https://elevenlabs.io → Profile → API Keys |
| **Rule of thumb** | ≈ **1 credit per character**, so ≈ **1,000 credits ≈ 1 minute** of narration. Starter ≈ 30 min/month, Creator ≈ 2 hours |

> ⚠️ **Turn on Pay-As-You-Go / Auto Top-Up in your ElevenLabs account.** By default, when
> your monthly credits run out the API **stops dead mid-generation** — we've seen a long
> video fail on its final chunk after the earlier ones were already paid for. Auto top-up
> prevents that.

### MiniMax — the cheaper alternative

| | |
|---|---|
| **Billing model** | 💳 Prepaid, **separate from their consumer "MiniMax Audio" app subscription** |
| **Minimum top-up** | **$5** |
| **Cost** | `speech-02-hd` **$100 per 1M characters** · `speech-02-turbo` **$60 per 1M** |
| **In plain terms** | ≈ **$0.10 per minute** of narration (HD), ≈ $0.06 (turbo) — roughly **half of ElevenLabs** |
| **Get the key** | https://platform.minimax.io/user-center/basic-information/interface-key |
| **Add funds** | https://platform.minimax.io/user-center/payment/balance |

> ⚠️ **Two things trip people up here.**
> **1.** MiniMax needs **both** an API key **and** a **Group ID** — the Group ID is on the
> same page, under **User Center → Basic Information**. Miss it and nothing works.
> **2.** Use the **global** site **platform.minimax.io**. There are China-region sites
> (`minimaxi.com`, `minimax.chat`) whose **keys are not interchangeable** — a key from the
> wrong one will simply be rejected.

### Other voice options

**69labs** — one gateway to three voice engines: **EdgeTTS** (Microsoft's free voices),
**ElevenLabs**, or **your own cloned voice**. Subscription from **$25/mo**, with a free tier
(5,000 characters/month) you can test on. Its headline TTS rate looks dramatically cheaper
than ElevenLabs — but that reflects the **EdgeTTS** engine, which does not sound like
ElevenLabs. Pick the engine deliberately in Settings, and judge by ear.

**GenAIPro** — an ElevenLabs reseller: same voices, different billing. **HeyGen** — handy
if you're already paying for an avatar. We haven't verified current rates for these two —
check their own dashboards before committing.

---

## 3. 🎨 AI visuals — pick ONE provider

Used when no real footage fits a scene. **Default: kie.ai.**

### kie.ai

| | |
|---|---|
| **Billing model** | 💳 Prepaid credits, pay-as-you-go — **no plans, no subscription, credits don't expire** |
| **Free credits** | Some are given at signup, **no card required** — but the amount isn't published, and it's small. Enough to try the Playground, not to render a video |
| **Top up from** | **$5** *(widely reported; not stated on their own page)* |
| **Credit rate** | 1 credit = **$0.005** |
| **Get the key** | https://kie.ai/api-key |
| **Add credits** | https://kie.ai/billing |

**What things cost** (from kie.ai's own pages — confirm in your dashboard):

| What | Price |
|---|---|
| Nano Banana **Pro** image (our default) | **$0.09** at 1K–2K · **$0.12** at 4K |
| Veo — **Fast**, clip up to 8s with audio | **$0.40 per clip** |
| Veo — **Quality**, clip up to 8s | **$2.00 per clip** |

> 📌 **Veo is priced per CLIP, not per second.** A clip up to 8 seconds costs the same
> whether it's 4s or 8s. So if you do use AI video, there's no saving in asking for shorter
> clips — and **Fast is 5× cheaper than Quality** for the same length. Default to Fast.

> 💰 **This is where all the money is.** A video's cost is driven almost entirely by whether
> AI fills a gap with an **image** or a **video clip**. For a 10-minute video (~130 scenes),
> if AI had to cover *every* scene:
>
> | AI media setting | Cost |
> |---|---|
> | **Images only** *(default)* | ≈ **$12** |
> | Video — Veo **Fast** | ≈ **$52** |
> | Video — Veo **Quality** | ≈ **$260** |
>
> In practice real footage covers most scenes, so the real number is much lower — but the
> *ratio* holds. **Keep "AI media" on "Images only"** unless you specifically want AI video
> and have budgeted for it. One operator left it on video and was surprised by a $40 bill.

### Magnific — works differently from the others

| | |
|---|---|
| **Billing model** | 📅 **Subscription only** — there is no pay-as-you-go, and **the free plan has no API access at all** |
| **Cheapest plan with an API key** | **Premium** (≈ €15/mo) · Premium+ **$39/mo** · Pro **$250/mo** |
| **Important** | Even on an "Unlimited" plan, **API calls still consume metered credits** — "unlimited" covers only their website |
| **Get the key** | https://www.magnific.com/user/api-keys |
| **Cost** | Per model, in credits: images from 1 to 2,100 credits; video 10–1,400 credits **per second** |

> Unlike kie.ai (top up $5, pay per use), Magnific needs a **monthly plan** before the API
> works at all. Fine if you already subscribe for their web tools — an odd fit if you just
> want a few images.

### 69labs

| | |
|---|---|
| **Billing model** | Monthly subscription (auto-renewing), plus optional one-time credit packs on top |
| **Free tier** | Yes, ongoing: ~**10 images** and ~**5 videos** per month, 5,000 TTS characters, files kept 1 day, no voice cloning |
| **Cheapest paid plan** | **$25/mo** (Starter) · credit packs from **$15** |
| **Sign up** | https://69labs.vip |

> Their **per-clip video cost isn't published anywhere public** — you only see credits-per-
> generation after signing up. Test on the free tier before committing to a plan.

---

## 4. 🖼️ Real footage — mostly free, and worth setting up

Real footage costs **nothing** and usually looks better than AI. Getting these two free
keys is the cheapest quality upgrade available.

| Source | Key needed | Where to get it | Limit |
|---|---|---|---|
| **Pexels** | free key | https://www.pexels.com/api/key *(log in first)* | 200 requests/hour, 20,000/month |
| **Pixabay** | free key | https://pixabay.com/api/docs/ — **the key is shown right on that page once you're logged in** | 100 requests/minute |
| **Wikimedia** | ❌ none | works out of the box | — |
| **Openverse** | ❌ none | works out of the box | — |
| **Archive.org** | ❌ none | works out of the box | — |
| **Library of Congress** | ❌ none | historical photos | strict — the app throttles itself |

No credit card is involved anywhere here, and **attribution is not legally required** for
either Pexels or Pixabay in your finished video (both are happy to be credited, but it's a
courtesy, not a condition).

> Without Pexels/Pixabay the app falls back to AI for almost every scene — which is both
> more expensive and less authentic. **Set these up first.**

> 📌 **On very long videos, mind Pexels' 200-requests-per-hour limit.** The app searches
> several sources per scene, so a 500-scene render can bump into it and start falling back
> to AI mid-way. If that happens, the fix is to add the **Pixabay** key as well so the load
> is shared — or split a very long video into parts.

> The optional `OPENVERSE_TOKEN` field can stay **empty**. Openverse works fine anonymously;
> a token only buys slightly higher limits and there's no simple signup form for it.

---

## 5. 👤 The presenter (HeyGen) — optional, and the biggest trap

**Skip this section entirely if you're making faceless videos.** Everything works without it.

| | |
|---|---|
| **Billing model** | 💳 Prepaid **API wallet**, **completely separate from your HeyGen website subscription** |
| **Does a web plan give API credits?** | ❌ **NO.** A Creator/Team subscription grants you **nothing** on the API |
| **Free API credits?** | ❌ **None** (removed February 2026) |
| **Minimum top-up** | **$5** |
| **Get the key + add credits** | https://app.heygen.com/settings/api → the API section of your account |

**What it costs per minute of avatar on screen:**

| Engine | Roughly |
|---|---|
| Legacy / "Unlimited" | **$1/min** |
| Avatar IV | **$3/min** |
| Avatar V | **$4/min** |

> 💡 The avatar only appears on ~15% of scenes, so a 10-minute video needs ~1.5 minutes of
> avatar — about **$1.50 on the cheapest engine**. Choosing a pricier engine multiplies that.
> Pick deliberately when you create the avatar.

**If your avatar silently doesn't appear in the finished video, it is almost always an
empty API wallet** — not a bug. Check the API balance, not your subscription.

---

## 6. 📝 Groq — only if you upload your own voiceover

If you record narration yourself and upload it, Groq transcribes it so the app knows where
each word falls. **Not needed if you let the app generate the voice.**

| | |
|---|---|
| **Billing model** | Postpaid — a card is charged for what you used. **No card needed to sign up** |
| **Free tier** | Generous: **8 hours of audio per day** (2 hours per hour), 2,000 requests/day. **Most people never pay for this at all** |
| **Cost if you exceed it** | **$0.111 per hour** of audio — fractions of a cent per video |
| **Get the key** | https://console.groq.com/keys |
| **Add a card (only if needed)** | https://console.groq.com/settings/billing |

> One limit worth knowing: on the free tier an uploaded file must be **under 25 MB**
> (100 MB once you add a card). Upload **mp3 / m4a**, not uncompressed WAV — a WAV hits
> that ceiling within a few minutes of audio, while an mp3 of the same length is tiny.

---

## 7. ☁️ Google Drive — optional auto-upload

Uploads finished videos to your Drive automatically. Fiddlier than the rest because you
create your own Google Cloud project.

If you see **"Request had insufficient authentication scopes"**, the permissions weren't
declared in your Google Cloud project. Fix:

1. **console.cloud.google.com** → your project → **APIs & Services → OAuth consent screen →
   Data Access** → **Add or Remove Scopes** → paste both:
   ```
   https://www.googleapis.com/auth/drive.file
   https://www.googleapis.com/auth/userinfo.email
   ```
2. **APIs & Services → Library** → enable **Google Drive API**.
3. If your consent screen is in **Testing**, add your own account under **Audience → Test users**.
4. In the app: **Disconnect**, then **Connect Google Drive** again, and **tick every
   permission checkbox** on Google's screen.

> The app's return address is fixed to **http://localhost:3000/api/gdrive/oauth/callback** —
> that exact URL must be listed in your OAuth client's **Authorized redirect URIs**, and the
> app must be running on port **3000**.

---

## The minimum to make your first video

**Faceless (no presenter):**
1. **Gemini** — key + **$10** deposit + billing ON ← *the one that breaks everything*
2. **Voice provider** — a paid plan if the video is commercial
3. **Pexels + Pixabay** — free keys
4. **kie.ai** — free signup credits are enough to start

**With a presenter:** add **HeyGen** and top up its **API wallet** (min $5) — remembering
that a HeyGen website subscription does **not** cover this.

---

## Rough cost of one 10-minute video

| | |
|---|---|
| Gemini | a few cents |
| Voice | part of your monthly plan (~10 min of your allowance) |
| Real footage | **free** |
| AI images filling the gaps (say 50 scenes) | ≈ **$4.50** |
| Presenter (~1.5 min on screen) | **$1.50** and up, depending on engine |
| **Typical total** | **around $6–10** |
| **If you switch AI media to video** | **$50–260** ← the one setting that changes everything |

---

## When something stops working, check billing first

| Symptom | Almost always |
|---|---|
| Footage is random / off-topic | Gemini billing not enabled (free-tier quota) |
| Avatar missing from the finished video | HeyGen **API wallet** empty (not the subscription) |
| Voiceover fails part-way through | ElevenLabs credits ran out mid-render — enable auto top-up |
| `402` / "insufficient credits" | That service's balance is at zero — top up |
| Mostly AI visuals when you asked for real | Pexels/Pixabay key missing |
| A surprisingly large bill | "AI media" was set to **video** instead of images |

---

*Prices here are what the providers published at the time of writing and can change —
your own dashboard is always the truth. Where a provider doesn't publish a figure, we've
said so rather than guessing.*
