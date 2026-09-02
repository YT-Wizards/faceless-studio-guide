# How to update the app (2 minutes)

> ✅ Don't worry: your **API keys, avatars, channels and finished videos are NOT deleted** by
> an update. They live in a separate folder (`~/.faceless-studio` on Mac,
> `C:\Users\YOU\.faceless-studio` on Windows), **not** inside the app folder.

---

## Steps

1. **Get the new version.** Your coach sends a **new ZIP** of the app, the same way you got the
   first one. There is nothing to download from a website.

2. **Stop the app** — close the black Terminal/CMD window if it's open.

3. **Unzip the new folder** and use it from now on. You can keep the old folder or delete it —
   your keys, avatars and videos are safe either way; they are stored outside the app folder.

4. **Run the installer once** in the new folder:
   - **Windows:** double-click **`install.bat`**.
   - **Mac:** double-click **`install.command`**.
     - ⚠️ If macOS says **"…is damaged and can't be opened"**: open the **Terminal** app, type
       `xattr -cr ` (with a space at the end), **drag the new app folder** into the window,
       press **Enter** — then double-click `install.command` again.

5. **Start the app:**
   - **Mac:** **`start.command`** · **Windows:** **`start.bat`**

6. **Windows, FFmpeg:** if you followed the guide and put ffmpeg's `bin` folder in
   `C:\Users\YOU\.faceless-studio\bin`, there is nothing to do — that folder is outside the
   app and survives the update. If you had copied it **into the old app folder** instead, move
   it to `.faceless-studio\bin` now, once, so you never have to think about it again.

> ℹ️ When an update needs something new, the next start installs it by itself and prints
> `[deps] package.json changed since the last install…` before the server comes up. That is
> normal and happens once per update.

---

## How to check the update worked

Create any video, open its page, and look at the **first line of the logs**:

```
Pipeline started (v0.5.0) · mode=mix · 4.5s/visual · avatar=15% · real=50%
```

If you see a **version number** like `(v0.5.0)` or newer — you're up to date. ✅
If the line has **no version number**, you're still on an old build; redo the steps above.

---

## What changed recently

Worth knowing when you open the new build and it doesn't look like the old one:

- **The Settings page mostly saves itself.** It opens as six one-line rows, in pipeline order,
  and shows only the keys the providers you picked actually need. A checkbox, a choice card or a
  dropdown is written the moment you click it; each API-key row has its own **Save** beside the
  box; and the **Save** on the title row is only for the typed fields that are left.
- **The Create page has three "look" tiles** for generated shots, all showing the same scene so
  the difference is the look and nothing else. One is badged **from Settings**.
- **The presenter can now appear *inside* ordinary shots**, not only as a talking head. It's a
  switch under the avatar picker, and it costs money per shot — see
  [BILLING.md §5](./BILLING.md).
- **Costs → "Check accounts"** asks kie.ai, HeyGen, 69labs and Magnific whether they still have
  credit (the other services have no balance endpoint — check those on their own dashboards).

Full details: [GUIDE-EN.md](./GUIDE-EN.md) · [BILLING.md](./BILLING.md)
