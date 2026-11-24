# VRFunScriptCast User Guide

**VR FunScriptCast** — a **native OpenXR** VR media player with funscript sync for Meta Quest 3 / PICO 4.
No Unity: rebuilt with Android + Kotlin/Compose + JNI C/OpenGL ES + OpenXR, playing local and LAN media
with 2D / 180° / 360° / fisheye projection, stereo layouts, video passthrough (MR keying) and toy sync.

![platforms](https://img.shields.io/badge/platform-Quest%203%20%7C%20PICO%204-8A2BE2) ![android](https://img.shields.io/badge/Android-10%2B-3DDC84) ![native](https://img.shields.io/badge/OpenXR-native-1E90FF)

**Download**: [Releases](https://github.com/wanfneg/VRFunScriptCast-Releases/releases) (single `arm64` APK, Quest / PICO).

> 中文版：[使用手册](user-guide.md)

---

## Known limitations

- Auto-detect samples the **current video frame**; when the subject color is close to the background, or the background has patterns/gradients, treat the result as a starting point and fine-tune with the mask preview.
- The transparent band of VR SPY-style sources under Alpha passthrough comes from the source's own mask layout — Skybox and other VR players reproduce it too; not optimized in this version.
- 2D-to-3D only applies to **flat-projection mono** videos; 180° / 360° / fisheye and side-by-side / top-bottom stereo are not supported, and it is off by default.
- The Handy motion is **beta**: custom stroke ranges (841) are not verified on hardware — keep the default 0–100 range and the emergency stop within reach.
- Quest 3 and PICO 4 family have both been run on real hardware; PICO models / OS versions vary a lot — include your device model and logs when reporting issues.

---

## Feature overview

### Playback & picture
- Sources: headset local folders + LAN sources (**SMB / WebDAV / DLNA**), unified hardware-decode pipeline with buffering retry and free seeking
- Projection formats: flat / equirectangular 180° / equirectangular 360° / fisheye 180° / fisheye 190° / lens-outline 200° / lens-outline 220°, switchable during playback
- Stereo layouts: top-bottom / half-width SBS / full-width SBS / mono
- Seven speed presets: 0.25× / 0.50× / 0.75× / 1.00× / 1.25× / 1.50× / 2.00×, each video starts at 1.00×; continuous playback, previous / next episode, retry on failure
- Buffering / seek hints live on a world-fixed hint rail (seek shows a picture preview)
- 8 built-in virtual scenes (Poly Haven CC0 HDRIs with previews and fixed orientations; 4K ASTC on Quest, 2K WebP fallback elsewhere), one tap to switch to the headset's real-environment passthrough
- Video passthrough (MR): green / blue / neutral-gray / light-gray chroma key + alpha channel + mask preview — chroma-keyed subjects can be overlaid on your real room
- The seek bar shows a funscript action heatmap — see "where the action is" at a glance

### Flat-video enhancements
- Halo / ambient glow: two separate layers, each with its own switch and strength; colours follow the video edge in real time, with a soft floor contact shadow
- 2D-to-3D (experimental): flat-projection mono only. Depth and parallax are estimated per frame on the headset; the video is never uploaded and no PC is needed. The 3D button in the player's top bar opens a popover with the on/off switch, Depth, Convergence and Reset. **Off by default**; enable Settings → Playback defaults → "Auto 3D for flat video" to start it automatically on flat mono videos
- AV1 software fallback (arm64 / Android 13+, 8-bit SDR): dav1d decodes when the platform decoder cannot

### funscript / device sync
- Script auto-matching (first hit wins):
  - Local videos: **same-directory same-name → local script folder → remote script folder**
  - Network videos: **network same-directory → local script folder → remote script folder**
  - Manual script picking in the file list / browse dialog is also supported
- Preset mode: 24 waveform presets + RANDOM shuffle + BOOST; stroke range and speed sliders in real time
- Quick actions: one-tap emergency stop / one-tap boost / idle easing / linkage control
- Script settings: delay adjustment, skip no-action segments, manual position, script folders
- Devices: BLE direct, TCode / OSR Bluetooth SPP direct, Intiface Central bridge, The Handy (FW4)
  - The Handy motion is beta: once connected and a script is playing it drives the device; default 0–100 stroke range, custom ranges (841) pending verification
- Device linking (BLE / The Handy / TCode / Intiface) requires a one-time activation license; playback and everything else stays free (see "Sponsor & License" in the README)
- **ServeU (抚物) device owners activate free**: no order ID needed — power on the device, keep it near the headset and tap "Activate via device" in Settings → Activation. Verification is automatic (once per install; app updates keep it)
- If automatic activation fails, contact the author on QQ `2831691505`

### Library & files
- Library shortcuts: cards for local folders and network sources, one tap to browse; scroll position is remembered per folder
- File browsing: directory / video / script / subtitle cards, distinguished by type icon and meta line
- Covers: local / network video thumbnails (cover-fill crop, in-memory cache); directory sort and scroll memory; per-file resume
- Subtitles: external `.srt` / `.ass` / `.ssa` auto-loaded by same name; embedded MKV subtitles (PGS / ASS etc.) render; the CC toggle controls both
- Three-source state sync: home page and player-page "Browse files" share library / local / network positions

### Interface & interaction
- Smoked-glass UI throughout with Noto Sans SC typography
- Settings → Controller guide: bilingual key-by-key tutorial
- Laser pointer + dot highlight, trigger to click, B / X to go back
- Thumbstick left/right flick for ±10s seek, hold for continuous fast seek (with picture preview); thumbstick up/down for view zoom (angular, no distortion)
- Hold grip to drag — move / rotate the playback window freely
- Player controls toggle with the trigger; the four dialogs are mutually exclusive and the bottom bar stays clickable

---

## Install

**Requirements**: Meta Quest 3 (Android 12+) or PICO 4 / PICO 4 Ultra (Android 10+); `arm64-v8a`; developer mode enabled.

1. Download the latest APK from [Releases](https://github.com/wanfneg/VRFunScriptCast-Releases/releases) (named like `VRFunScriptCast-<version>-arm64.apk`).
2. Same-signature builds upgrade in place; upgrading from the old Unity build or test builds has a different signature — **uninstall first** (in-app data will be cleared).
3. Sideload with SideQuest on PC, or install via adb:

```powershell
adb install -r VRFunScriptCast-<version>-arm64.apk
```

First launch requests **storage permission** (browse local videos) and **Bluetooth permission** (connect devices); the corresponding features are unavailable if denied.

---

## Quick start

### Home

Four entries on the bottom bar:

| Entry | Content |
|---|---|
| **Library** | Shortcuts: cards for local folders and network sources, tap to browse |
| **Local files** | Browse the headset's local storage; the top bar offers "set as local script folder" |
| **Network sources** | Configure SMB / WebDAV / DLNA video and script sources |
| **Settings** | Playback (delay, skip no-action, idle easing, manual position, playback defaults, script folders), Device (Intiface bridge, TCode / OSR), App (activation, controller guide, about) |

Bottom bar left: device connection, scene, passthrough; right: exit.

### Network sources

Tap "Add source" or a card's "Edit" on the network sources page:

- **WebDAV**: full URL (e.g. `http://192.168.1.5:11501/dav`), account, password
- **SMB**: host IP, share name (leave empty to list shares), account, password
- **DLNA**: tap "Scan devices" to pick one, or enter a `description.xml` URL

After saving, tap the card's "Browse" to enter the directory. Video and script may come from two different sources/protocols.

### Playback

- Tap a video on the home page to play; the player's "Browse files" switches videos within the current source without going back home.
- Continuous playback: when a video ends, the next one in the same folder plays automatically (toggle in Settings → skip panel, on by default); the previous / next episode buttons beside ±10s grey out when there is no adjacent video.
- Speed: the speed chip in the player controls opens a seven-step panel (0.25× / 0.50× / 0.75× / 1.00× / 1.25× / 1.50× / 2.00×); every video starts at 1.00×.
- The playback-failure banner offers "Retry" to replay the last request; if no script auto-matches, you can browse and load one manually.
- Player bottom bar: **Home / Browse files / Video passthrough / Boost / Emergency stop / Idle easing / Linkage / Presets**.
- Top bar left: device pill (connect / disconnect during playback); right: passthrough / scene / CC.
- Format row: projection / stereo / load-script buttons; projection is re-detected for each new video.

### Flat-video enhancements (glow / 2D-to-3D)

Only shown for **flat-projection mono** videos, in the player's top bar:

- **Halo / Ambient**: each button opens its own popover with an on/off switch and a "Light strength" slider (percentage). Colours follow the video edge in real time; Ambient is on by default, Halo is off.
- **3D**: the button only opens the adjustment popover — the switch and sliders live inside it (same interaction as Ambient). It shows the "Experimental 3D: flat mono only, processed on this device" note, an on/off switch, Depth, Convergence and Reset. Button states: `3D…` while the model loads, `3D ✓` when ready.
- Defaults: 3D is **off by default**; Settings → Playback defaults → "Auto 3D for flat video" is also off by default and, when enabled, starts 3D automatically on flat mono videos.

### Script loading

Put a `.funscript` in the video's folder with the same name and it loads automatically. Also supported:

1. Set a directory as the **local script folder** on the "Local files" page (indexed recursively);
2. Configure a **remote script source** on the "Network sources" page (the script folder);
3. Pick a script manually in the player's "Browse files".

Priority is listed under "funscript / device sync" above. The network same-directory always wins over the local script folder for network videos.

### Device connection

Tap the device pill on the home / player page → choose a device to connect. Grant Bluetooth permission on first use; the device must be powered on and not occupied by another app.
The device dialog scans / connects devices and shows status; The Handy (FW4) uses the same entry and drives the device once a script plays (motion is beta — keep the default 0–100 range). Stroke range, speed limit, invert and OC are adjusted in the linkage / preset dialogs.

### Video passthrough (MR keying)

Player page "Video passthrough":

- Modes: off / green screen / blue screen / neutral gray / light gray / alpha channel / mask preview
- Color tolerance and edge feathering sliders in real time; "Auto detect" samples the dominant color from the outer ring of the current frame, switches between hue-key / solid-color key automatically, and persists across video change / restart
- Enabling keying turns on the passthrough background — your real room shows through the keyed area
- Alpha channel is for sources with packed alpha

---

## FAQ

- **In-place upgrade fails**: the old Unity build / test builds have a different signature — uninstall the old one, then install the latest from this repo; native builds in this repo share one signature and upgrade in place.
- **No local videos**: grant this app storage permission in system settings and come back.
- **Network source won't connect**: make sure the headset and the NAS / PC are on the same LAN; check IP, account and password; for SMB, leave the share name empty to list shares first.
- **DLNA won't enter**: the DLNA service may not be running; re-scan / enter the description URL via "Edit" on the network sources page.
- **Device won't connect**: make sure the device is powered on, charged, and its Bluetooth is not occupied by another phone app; tap the device pill to retry.
- **How do I activate device linking?** ServeU (抚物) device → Settings → Activation → "Activate via device" (automatic); other devices → Settings → Activation → paste your Afdian order ID / Ko-fi transaction ID → tap Claim.
- **How do I enable 2D-to-3D?** The top-bar "3D" button only appears for flat-projection mono videos; open its popover and switch it on, or enable Settings → Playback defaults → "Auto 3D for flat video". 180°/360°/fisheye and stereo are not supported.
- **The Handy doesn't move**: make sure it is connected and a script is playing; motion is beta — keep the default 0–100 range and the emergency stop within reach.
- **AV1 won't play**: the software fallback only covers arm64 / Android 13+ 8-bit SDR AV1; otherwise the platform decoder must support it.
- **Black or distorted picture**: switch projection / stereo format on the player page; playback failures show a red banner.
