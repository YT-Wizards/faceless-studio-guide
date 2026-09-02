# Paying for the services — what to set up, and in what order

> **Read this before your first video.** Almost every "it doesn't work" message turns out to be
> a billing setup that was never finished. The app itself is free; you pay the AI services
> directly, and **most of them bill their API separately from their normal subscription.**
> That surprise is the single most common blocker.
>
> 📖 Making the video itself: [GUIDE-EN.md](./GUIDE-EN.md)

---

## The one rule that catches everyone

> **A normal subscription on a service's website does NOT automatically give you API access.**

Several of these companies run two separate wallets: one for using their website, and one for
programs (like this app) talking to them. Paying for the first does nothing for the second.
**HeyGen works exactly this way** — it is the #1 thing people get stuck on.

Each section below says which model that service uses.

---

## Three ways these services charge

| Model | What it means | Who does it |
|---|---|---|
| 💳 **Prepaid** | You deposit money; usage draws it down; at zero it just stops | Gemini · kie.ai · HeyGen API · MiniMax · GenAIPro |
| 📅 **Subscription** | Monthly plan with an included allowance; the API draws from the same pool | ElevenLabs · Magnific · 69labs · Storyblocks |
| 🆓 **Free** | Just a key, or not even that | Pexels · Pixabay · Wikimedia · Openverse · Archive.org · Wigolo · Groq (in practice) |

**Prepaid is your friend.** You cannot overspend — when the balance hits zero, generation
stops. Don't turn on auto-reload until you know your monthly volume.

> 🔎 **The app can ask for you.** **Costs → "Check accounts"** probes the providers that expose a
> balance — **kie.ai, HeyGen, 69labs and Magnific** — and reports whether each still has credit.
> The other services (ElevenLabs, Gemini, the footage sources…) have no such endpoint, so check
> those on their own dashboards. Every probe is free and generates
> nothing. An account that has run dry looks exactly like a source that found nothing, so this
> button is usually the fastest answer to "why did the quality drop?".

---

## 1. 🧠 Google Gemini — the one that decides whether your video is any good

Gemini picks what appears on screen for each sentence.

**Its failure mode is the important part.** Without the key the app does **not** stop — it
falls back to searching your sentence word-for-word, and the footage comes out literal and
off-topic. On the free tier the quota runs out after a few shots and the rest of the video
degrades the same way. Neither looks like an error; both look like "the app is bad".

| | |
|---|---|
| **Billing model** | 💳 Prepaid deposit (the default for new accounts) |
| **Minimum** | **$10** |
| **Free tier** | Exists, but the quota is far too small for a real video |
| **Get the key** | https://aistudio.google.com/app/apikey |
| **Add money** | Same place — billing is managed inside AI Studio |
| **What it costs you** | A few cents to a couple of dollars per video |

> ⚠️ **A Google One / Gemini Advanced subscription does NOT count.** That's a consumer plan and
> does nothing for the API. You need **API billing** specifically. People lose days to this.

**Do this:** create the key → enable billing → deposit $10 → paste it into Settings. Leave
auto-reload OFF at first.

*(The same key also powers the app's quality check on generated pictures and the watermark
guard. Without it those simply pass everything through unchecked.)*

---

## 2. 🎙️ The voice — pick ONE provider

Nine are supported. **You only need a key for the one you choose** in
**Settings → Voice provider** — or none at all if you upload your own narration (§6).

### ElevenLabs — the default, best-known

| | |
|---|---|
| **Billing model** | 📅 Subscription. **The API and the website share ONE credit pool** — there is no separate API balance |
| **Free tier** | 10,000 credits/month, and the API does work on it — **but free-tier output cannot be used commercially** |
| **For commercial use** | Any paid plan: Starter **$6/mo** (30k credits) · Creator **$22/mo** (121k) · Pro **$99/mo** (600k) |
| **Get the key** | https://elevenlabs.io → Profile → API Keys |
| **Rule of thumb** | ≈ **1 credit per character**, so ≈ **1,000 credits ≈ 1 minute** of narration. Starter ≈ 30 min/month, Creator ≈ 2 hours |
| **App's assumed rate** | $0.22 per 1,000 characters |

> ⚠️ **Turn on Pay-As-You-Go / Auto Top-Up in your ElevenLabs account.** By default, when your
> monthly credits run out the API **stops dead mid-generation** — a long video can fail on its
> final chunk after the earlier ones were already paid for.

### MiniMax — the cheaper alternative

| | |
|---|---|
| **Billing model** | 💳 Prepaid, **separate from the consumer "MiniMax Audio" app subscription** |
| **Minimum top-up** | **$5** |
| **Cost** | `speech-02-hd` **$100 per 1M characters** · `speech-02-turbo` **$60 per 1M** |
| **In plain terms** | ≈ **$0.10 per minute** of narration (HD), ≈ $0.06 (turbo) — roughly **half of ElevenLabs** |
| **Get the key** | https://platform.minimax.io/user-center/basic-information/interface-key |
| **Add funds** | https://platform.minimax.io/user-center/payment/balance |

> ⚠️ **Two things trip people up here.**
> **1.** MiniMax needs **both** an API key **and** a **Group ID** — the Group ID is on the same
> page, under **User Center → Basic Information**. Miss it and nothing works; the app shows
> both fields side by side for exactly this reason.
> **2.** Use the **global** site **platform.minimax.io**. There are China-region sites
> (`minimaxi.com`, `minimax.chat`) whose **keys are not interchangeable** — a key from the
> wrong one is simply rejected.

### The resellers — one key, several engines

**AI84** fronts **ElevenLabs *and* MiniMax** behind one key. The **model** you pick in Settings
is what decides which engine you're on — pick an `eleven_*` model and you're on ElevenLabs, a
`speech-*` model and you're on MiniMax. **Cloned voices exist only on the MiniMax side**; a
cloned voice sent to the ElevenLabs engine comes back as "voice not found".

**ai33.pro (OpenSpeaker)** fronts **six** engines — clone / ElevenLabs / MiniMax / Fish Audio /
Edge / Vbee. There is nothing extra to configure: the engine travels inside the voice id, so
choosing a voice from the picker chooses the engine with it.

**GenAIPro** — an ElevenLabs reseller: same voices, different billing.

| | |
|---|---|
| **Billing model** | 💳 Prepaid credit packs — **no subscription, no auto-renewal** |
| **Minimum** | **$8** (250,000 credits, valid 30 days) |
| **Get the key** | **genaipro.io** → sign in → Avatar → **Manage Account → API Key** |

> ⚠️ **Use exactly `genaipro.io`.** Several similar domains exist (`.co`, `.cc`, `.co.in`,
> `.vn`) that are unrelated sites. Check the address bar before entering payment details.

> For all three resellers: their price for the **ElevenLabs** voices specifically is not
> published, and their in-house voices are much cheaper but are different voices. **Buy the
> smallest pack first**, generate one test, and look at what it actually consumed before
> topping up. The app ships these providers' rate fields **empty**, so their spend shows as
> "rate not set" on the Costs page until you fill in what your own dashboard says.

### The rest

| Provider | What to know |
|---|---|
| **Fish Audio** | Bills per **million UTF-8 bytes** — so non-Latin scripts cost roughly twice what the character count suggests. The app assumes **$15 per 1M bytes**. |
| **Hume AI (Octave)** | Bills per 1,000 characters; the app assumes **$0.15**. Octave-2 voices need `HUME_VERSION = 2` — the voice picker flags a mismatch rather than letting the run fail. |
| **69labs** | One gateway to EdgeTTS (Microsoft's free voices), ElevenLabs, or your own cloned voice. Subscription from **$25/mo**, free tier 5,000 characters/month. Its headline rate looks dramatically cheaper than ElevenLabs — that reflects **EdgeTTS**, which does not sound like ElevenLabs. Pick the engine deliberately and judge by ear. |
| **HeyGen** | Handy if you already pay for the avatar. Same **API wallet** as §5 — the same trap applies. Rates not separately verified. |

---

## 3. 🎨 AI visuals — pick ONE provider

Used when no real footage fits a shot, and for everything in **Full AI** mode.
**Default: kie.ai.**

### kie.ai — the default

| | |
|---|---|
| **Billing model** | 💳 Prepaid credits, pay-as-you-go — **no plans, no subscription, credits don't expire** |
| **Free credits** | Some at signup, no card required — small; enough to try, not to render a video |
| **Top up from** | **$5** *(widely reported; not stated on their own page)* |
| **Credit rate** | 1 credit = **$0.005** |
| **Get the key** | https://kie.ai/api-key |
| **Add credits** | https://kie.ai/billing |

**What things cost:**

| What | Price |
|---|---|
| Nano Banana **Pro** image — *the app's default picture, and what cameos use* | **$0.09** |
| **Nano Banana** image — the cheaper tier, one click away in Settings → AI visuals | **$0.02** |
| **Veo 3 Fast** clip, up to 8s | **$0.325 per clip** |
| Veo **Quality** clip, up to 8s | **$2.00 per clip** |

> 📌 **Two things worth knowing, both measured against a real account rather than read off a
> price page.**
> **Veo is priced per CLIP, not per second** — a clip costs the same whether it's 4s or 8s, so
> asking for shorter clips saves nothing. And **kie's own page still advertises $0.40** for the
> Fast tier while the account is actually charged **$0.325**; the app uses the measured figure.
> **Fast is about 6× cheaper than Quality** for the same length. Default to Fast.

> 💰 **This is where all the money is.** A video's cost is driven almost entirely by whether AI
> fills a gap with an **image** or a **video clip**. For a 10-minute video (~130 shots), if AI
> had to cover *every* shot:
>
> | AI media setting | Cost |
> |---|---|
> | **Images only** *(the default)* | ≈ **$2.60** |
> | Video — Veo **Fast** | ≈ **$42** |
> | Video — Veo **Quality** | ≈ **$260** |
>
> In practice real footage covers most shots, so the real number is far lower — but the *ratio*
> holds. **Keep "AI media" on "Images only"** unless you specifically want AI video and have
> budgeted for it.

### Magnific — works differently from the others

| | |
|---|---|
| **Billing model** | 📅 **Subscription only** — no pay-as-you-go, and **the free plan has no API access at all** |
| **Cheapest plan with an API key** | **Premium** (≈ €15/mo) · Premium+ **$39/mo** · Pro **$250/mo** |
| **Important** | Even on an "Unlimited" plan, **API calls still consume metered credits** — "unlimited" covers only their website |
| **Get the key** | https://www.magnific.com/user/api-keys |
| **App's assumed rates** | $0.119 per image · $0.35 per video clip — both *published estimates*, never checked against an invoice |

### 69labs

| | |
|---|---|
| **Billing model** | Monthly subscription (auto-renewing), plus optional one-time credit packs |
| **Free tier** | Yes, ongoing: ~**10 images** and ~**5 videos** per month, 5,000 TTS characters, files kept 1 day, no cloning |
| **Cheapest paid plan** | **$25/mo** (Starter) · credit packs from **$15** |
| **Sign up** | https://69labs.vip |

> 69labs **states the amount it actually charged** for pay-per-use accounts, and the app records
> that figure rather than guessing — so on such an account no rate needs filling in at all. On a
> **credit** account you need to supply one number (the price you paid per credit). The app asks
> 69labs which of the two you're on instead of assuming.
>
> Their per-clip video cost is not published anywhere public. Test on the free tier first.

### Runware and Higgsfield

Both are supported and neither publishes a rate this app can safely assume, so both ship with
their rate fields **empty** and their spend reads "rate not set" until you fill it in.

- **Runware** *(marked Experimental)* reports its **real billed amount** per image, so once
  you're generating, the Costs page shows genuine money for it without any rate at all. Its
  catalogue spans a ~100× price range — from ~$0.0013 to ~$0.138 per image — so the model you
  pick matters far more than the provider does.
- **Higgsfield** needs a key **and** a secret (two fields). How it bills its DoP video model is
  unverified; take the figure from your own dashboard.

---

## 4. 🖼️ Real footage — mostly free, and worth setting up first

Real footage usually looks better than AI **and costs nothing**. These free keys are the
cheapest quality upgrade available anywhere in this app.

| Source | Key needed | Where to get it | Limit |
|---|---|---|---|
| **Pexels** | free key | https://www.pexels.com/api/key *(log in first)* | 200 requests/hour, 20,000/month |
| **Pixabay** | free key | https://pixabay.com/api/docs/ — **the key is shown on that page once you're logged in** | 100 requests/minute |
| **Wikimedia** | ❌ none | works out of the box | — |
| **Openverse** | ❌ none | works out of the box | — |
| **Archive.org** | ❌ none | works out of the box | — |
| **Wigolo** | ❌ none, no signup | works out of the box — a small helper the app starts for itself | — |
| **Brave** | ✅ `BRAVE_API_KEY` | ~$5 per 1000 searches, billed on the request (a 4xx is charged too). Roughly $0.17 a 3-minute video. Brave withdrew its free tier in Feb 2026, and its $5/mo credit needs public attribution a local install cannot give. Wigolo covers the same ground for free. | https://api-dashboard.search.brave.com |
| **Web (Google)** | 2 keys | a Google **Custom Search** key + engine id (`cx`) | 100 free queries/day |
| **Storyblocks** | 💳 **paid**, a key **pair** | https://developer.storyblocks.com | your plan's download quota |

No credit card is involved for the free ones, and **attribution is not legally required** for
Pexels or Pixabay in your finished video (both are happy to be credited — a courtesy, not a
condition).

> **Without Pexels/Pixabay the app falls back to AI for almost every shot** — more expensive
> and less authentic. **Set these up first.**

> 📌 **On very long videos, mind Pexels' 200-requests-per-hour limit.** The app searches several
> sources per shot, so a 500-shot render can bump into it and start falling back to AI part-way.
> Two fixes, both supported: **add several Pexels keys** (the Settings field takes a list and
> the app rotates them), and add **Pixabay** so the load is shared. Or split a very long video
> into parts.

> **Storyblocks is the only paid source, and only DOWNLOADS cost money — searching is free.**
> Its free test tier is **5 downloads in total** (not per day) against 1,000 searches a day, so
> it runs out almost immediately without a paid plan. Storyblocks exposes no quota endpoint, so
> the app counts locally: set `STORYBLOCKS_MAX_DOWNLOADS_PER_RUN` in full settings (0 = no cap)
> if you want to be sure one long video can't drain a month.

> The optional `OPENVERSE_TOKEN` field can stay **empty**. Openverse works fine anonymously; a
> token only buys slightly higher limits.

---

## 5. 👤 The presenter (HeyGen) — optional, and the biggest trap

**Skip this section entirely for faceless videos.** Everything works without it.

| | |
|---|---|
| **Billing model** | 💳 Prepaid **API wallet**, **completely separate from your HeyGen website subscription** |
| **Does a web plan give API credits?** | ❌ **NO.** A Creator/Team subscription grants you **nothing** on the API |
| **Free API credits?** | ❌ **None** |
| **Minimum top-up** | **$5** |
| **Get the key + add credits** | https://app.heygen.com/settings/api |

**What it costs per minute of presenter *talking on camera*:**

| Engine | Rate |
|---|---|
| **Legacy** | **$1/min** |
| **Avatar IV** *(recommended)* | **$3/min** |
| **Avatar V** | **$4/min** — *an estimate; HeyGen publishes no price for this combination* |

> 💡 He only talks on ~15% of the shots, so a 10-minute video needs ~1.5 minutes of avatar —
> about **$1.50 on Legacy**, **$4.50 on Avatar IV**. You choose the engine once, when you create
> the avatar, and it applies to every video that avatar appears in.

**If the presenter silently doesn't appear in the finished video, it is almost always an empty
API wallet** — not a bug. Check the **API balance**, not your subscription. The app reads
that wallet at both ends of every run and writes the difference into the run's log
("HeyGen wallet spend during this run").

### The presenter *inside* the shots (cameos) — a separate bill

This is a different feature from the talking head, and it is **not** billed by HeyGen. Each
cameo frame is generated by your **AI image provider** from the reference photo:

| | |
|---|---|
| **What it costs** | ~**$0.09** per still on the default backend (kie.ai Nano Banana Pro) |
| **If you also switch on "Moving clip"** | roughly **$0.28–0.35 more per shot**, and around **two extra minutes of render time** each |
| **Who can do it** | kie.ai *(default)* · Magnific · Higgsfield · 69labs · Runware — set in **Settings**, and it does **not** have to be the same provider you chose in §3 |

At the shipped 35%, a 130-shot video has roughly 45 cameo frames ≈ **$4** as stills, or **$16+**
as moving clips. Start with stills.

---

## 6. 📝 Groq — only if you upload your own voiceover

If you record narration yourself and upload it, Groq transcribes it so the app knows where each
word falls. **Not needed if you let the app generate the voice** — though it also sharpens the
timing of synthesized narration on every provider except ElevenLabs.

| | |
|---|---|
| **Billing model** | Postpaid — a card is charged for what you used. **No card needed to sign up** |
| **Free tier** | Generous: **hours of audio per day**. Most people never pay for this at all |
| **Cost if you exceed it** | **$0.111 per hour** of audio — fractions of a cent per video |
| **Get the key** | https://console.groq.com/keys |
| **Add a card (only if needed)** | https://console.groq.com/settings/billing |

> The app's **50-minute** upload cap comes straight from Groq's 25 MB request limit. Upload
> **mp3 / m4a**, not uncompressed WAV — a WAV hits that ceiling within a few minutes of audio,
> while an mp3 of the same length is tiny. A normal mp3 narration always fits.

---

## 7. ☁️ Google Drive — optional auto-upload

Uploads finished videos to your Drive automatically. Fiddlier than the rest because you create
your own Google Cloud project. Set it up in **full settings**.

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
4. In the app: **Disconnect**, then **Connect Google Drive** again, and **tick every permission
   checkbox** on Google's screen.

> The app's return address is fixed to **http://localhost:3001/api/gdrive/oauth/callback** —
> that exact URL must be listed in your OAuth client's **Authorized redirect URIs**, and the app
> must be running on port **3000**.

---

## The minimum to make your first video

**Faceless (no presenter):**
1. **Gemini** — key + **$10** deposit + billing ON ← *the one that decides whether it's any good*
2. **A voice provider** — a paid plan if the video is commercial
3. **Pexels** (+ Pixabay) — free keys
4. **kie.ai** — the signup credits are enough to start

**With a presenter talking on camera:** add **HeyGen** and top up its **API wallet** (min $5) —
remembering that a HeyGen website subscription does **not** cover this.

**With the presenter inside the shots too:** nothing new to buy — those frames come out of your
AI provider's balance (§5).

**Uploading your own narration instead:** swap step 2 for a free **Groq** key.

---

## Rough cost of one 10-minute video

| | |
|---|---|
| Gemini | a few cents |
| Voice | part of your monthly plan (~10 min of your allowance) |
| Real footage | **free** |
| AI images filling the gaps (say 50 shots) | ≈ **$1.00** |
| Presenter talking (~1.5 min on screen) | **$1.50** (Legacy) to **$4.50** (Avatar IV) |
| Presenter cameos as stills (~45 shots at 35%) | ≈ **$4** |
| **Typical total** | **$3–10**, depending on how much of the presenter you use |
| **If you switch AI media to video** | **$40–260** ← the one setting that changes everything |
| **If you switch cameos to moving clips** | **+$12–16** on top |

The **Costs** page reports all of this in **US dollars** — every provider bills in USD, and
nothing is converted.

---

## When something stops working, check billing first

| Symptom | Almost always |
|---|---|
| Footage is random / off-topic | Gemini key missing, or its billing not enabled (free-tier quota) |
| Presenter missing from the finished video | HeyGen **API wallet** empty (not the subscription) |
| Voiceover fails part-way through | ElevenLabs credits ran out mid-render — enable auto top-up |
| `402` / "insufficient credits" | That service's balance is at zero — top up |
| Mostly AI visuals when you asked for real | Pexels/Pixabay key missing, or Pexels' hourly limit hit |
| Quality dropped for no visible reason | A provider ran dry and the app fell through to the next. **Costs → Check accounts** |
| A surprisingly large bill | "AI media" was set to **video**, or cameos to **moving clip** |
| The Costs page says "rate not set" | Nobody has that price. Put what your invoice says into the rate field — the page recalculates **all** past runs, so old totals will legitimately move |

---

*Prices here are what the providers published at the time of writing, except where this guide
says a figure was measured against a live account — those are what the account was actually
charged. Providers change pricing; your own dashboard is always the truth. Where a provider
doesn't publish a figure, this guide says so rather than guessing.*
