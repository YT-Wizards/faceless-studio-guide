# How to update the app (2 minutes)

> ✅ Don't worry: your **API keys, avatars, channels and finished videos are NOT
> deleted** by an update. They live in a separate folder (`~/.faceless-studio` on
> Mac, `C:\Users\YOU\.faceless-studio` on Windows), **not** inside the app folder.

---

## Steps

1. **Get the new version.** Your coach will send you a **new ZIP** of the app
   (the same way you got the first one). There's nothing to download from a website.

2. **Stop the app** — close the black Terminal/CMD window if it's open.

3. **Unzip the new folder** and use it from now on (you can keep the old folder or
   delete it — your keys/avatars/videos are safe either way, they're stored outside
   the app folder).

4. **Run the installer once** in the new folder:
   - **Windows:** double-click **`install.bat`**.
   - **Mac:** double-click **`install.command`**.
     - ⚠️ If macOS says **"…is damaged and can't be opened"**: open the **Terminal**
       app, type `xattr -cr ` (with a space), **drag the new app folder** into the
       window, press **Enter** — then double-click `install.command` again.

5. **Start the app:**
   - **Mac:** **`start.command`** · **Windows:** **`start.bat`**

6. *(Windows only, if you set up FFmpeg by copying its `bin` folder)* copy that
   `bin` folder into the new app folder too — or keep FFmpeg installed system-wide.

---

## How to check the update worked

Create any video, open its page and look at the **first line of the logs**:

```
Pipeline started (v0.4.2) · ...
```

If you see a **version number** like `(v0.4.2)` (or newer) — you're up to date. ✅
If the line has **no version number** — you're still on an old build; redo the steps above.
