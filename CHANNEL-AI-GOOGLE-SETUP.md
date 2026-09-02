# YouTube Channel AI VIP — connecting Google

> This page is about the **analytics app** (YouTube Channel AI VIP), not the video
> generator. If you're setting up the Faceless Video Generator, you want
> **[GUIDE-EN.md](./GUIDE-EN.md)** instead.

The analytics app talks to Google in two different ways, and they are easy to mix up:

| What you set up | What it unlocks | Needed? |
|---|---|---|
| **An API key** | Adding channels, reading public data on you and your competitors — views, titles, thumbnails, likes | **yes** |
| **A Google sign-in (OAuth)** | Your own private numbers — watch time, retention, revenue, and **thumbnail click-through rate** | optional, but it's where the good stuff is |

---

## Turn on three APIs — not one

All three live in the **same** Google Cloud project. Left menu →
**APIs & Services → Library** → search the name → **Enable**.

| API | Why you need it | If you skip it |
|---|---|---|
| **YouTube Data API v3** | Adding channels at all | The app can't add a channel |
| **YouTube Analytics API** | Views over time, retention, traffic, revenue | Those panels stay empty |
| **YouTube Reporting API** | **Thumbnail impressions and click-through rate** | Everything works, but the thumbnail tools rank your covers by **views** instead of by **clicks** |

The third one is the one people miss. It's off by default, it isn't the same service as
the other two, and nothing tells you it's missing until you look.

---

## Why click-through is worth turning on early

**Views tell you the topic worked. Click-through tells you the picture worked.** That's
the number the thumbnail tools want: out of everyone who was *shown* your cover, how many
actually clicked it. The app uses it to work out which of your thumbnails genuinely earn
clicks, and to learn your channel's winning style from those instead of from whatever
happened to go viral.

Three things about it are worth knowing before you wait around wondering if it's broken:

- **The first data can take up to 48 hours.** Google doesn't answer this one on the spot —
  it prepares a file once a day, and it doesn't start until you enable the API. Nothing is
  wrong in the meantime.
- **Google only backfills 30 days.** History older than 30 days before the day you turned
  it on is gone for good. So turn it on now even if you don't care about thumbnails yet —
  it costs nothing and it's the only way to have history later.
- **Your computer does not need to be running.** Google keeps each daily file on its side
  for 60 days. Close the app for three weeks and it will collect all three weeks the next
  time you open it. Just don't leave it closed for more than two months.

**Click-through is yours alone.** Nobody — not this app, not any other tool — can see a
competitor's click-through rate. It's private to the channel's owner. Competitor
thumbnails are judged on views instead, and the app says so rather than pretending the two
are the same evidence.

---

## Signing in with Google

1. **APIs & Services → OAuth consent screen**
   - **User Type**: External → **Create**
   - Fill in app name and your email for both contact fields.
   - **Scopes** → add all three:
     - `https://www.googleapis.com/auth/yt-analytics.readonly`
     - `https://www.googleapis.com/auth/yt-analytics-monetary.readonly`
     - `https://www.googleapis.com/auth/youtube.readonly`
   - **Audience** → **Publish app**, so the status reads **In production**.

   > ⚠️ **Publish it — don't add yourself as a "test user".** An app left in *Testing* has
   > its connection dropped by Google **every 7 days**, and you'll be reconnecting forever.
   > Publishing takes one click and does **not** require Google to review anything for an
   > app only you use.

2. **APIs & Services → Credentials → + Create Credentials → OAuth client ID**
   - **Application type**: Web application
   - **Authorized redirect URIs** → add **exactly** this, no trailing slash:
     ```
     http://localhost:3010/api/youtube/oauth/callback
     ```
     It must be `http://`, not `https://` — this is your own computer.

   > If Google says **"Access blocked: this app's request is invalid"** with
   > `Error 400: redirect_uri_mismatch`, this is the line that's wrong — usually because
   > the app is running on a different port than the one you registered. Whatever address
   > the app opens in your browser is the one that has to be in this box.

3. In the app: **Settings** → paste **Client ID** and **Client secret** → **Save**.
4. Then click **Connect** next to each channel and sign in with **that channel's owner
   account**.

   > ⚠️ **Editor or Manager access is not enough.** Google blocks invited users from the
   > YouTube APIs no matter what they can see in Studio
   > ([Google's own rule](https://support.google.com/youtube/answer/9481328)). It has to be
   > the owner. Check who that is in **YouTube Studio → Settings → Permissions**.
   >
   > **On a Brand Account**, sign in with the personal Google account that owns it — a
   > Brand Account has no login of its own. Google will then show you a channel picker.

---

## How to tell it worked

- **Channels sync and show videos** → the API key is fine.
- **Views, retention and revenue appear** → the sign-in is fine.
- **The thumbnail tools say they ranked your covers by click-through** rather than by views
  → the Reporting API is fine and the data has arrived. Until then they say "views", which
  is honest, not broken.

If revenue shows for one channel and not another, that is usually not a bug: Google refuses
revenue for channels you don't own at the required level, and for channels that aren't in
the Partner Programme.
