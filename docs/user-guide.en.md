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
- Quest 3 and PICO 4 family have both been run on real hardware; PICO models / OS versions vary a lot — include your device model and logs when reporting issues.

---

## Feature overview

### Playback & picture
- Sources: headset local folders + LAN sources (**SMB / WebDAV / DLNA**), unified hardware-decode pipeline with buffering retry and free seeking
- Projection formats: flat / equirectangular 180° / equirectangular 360° / fisheye 180° / fisheye 190° / lens-outline 200° / lens-outline 220°, switchable during playback
- Stereo layouts: top-bottom / half-width SBS / full-width SBS / mono
- 8 built-in virtual scenes, one tap to switch to the headset's real-environment passthrough
- Video passthrough (MR): green / blue / neutral-gray / light-gray chroma key + alpha channel + mask preview — chroma-keyed subjects can be overlaid on your real room
- The seek bar shows a funscript action heatmap — see "where the action is" at a glance

### funscript / device sync
- Script auto-matching (first hit wins):
  - Local videos: **same-directory same-name → local script folder → remote script folder**
  - Network videos: **network same-directory → local script folder → remote script folder**
  - Manual script picking in the file list / browse dialog is also supported
- Preset mode: 24 waveform presets + RANDOM shuffle + BOOST; stroke range and speed sliders in real time
- Quick actions: one-tap emergency stop / one-tap boost / idle easing / linkage control
- Script settings: delay adjustment, skip no-action segments, manual position
- Device management: Bluetooth connection, stroke range / speed limit / invert / boost mode (OC), device info, Wi-Fi firmware OTA
- Device linking (BLE / TCode / Intiface) requires a one-time activation license; playback and everything else stays free (see "Sponsor & License" in the README)
- **ServeU (抚物) device owners activate free**: if you already own a ServeU device you don't need to buy a license — add QQ `2831691505` to get your activation code

### Library & files
- Library shortcuts: cards for local folders and network sources, one tap to browse; scroll position is remembered per folder
- File browsing: directory / video / script / subtitle cards, distinguished by type icon and meta line
- External subtitles: `.srt` / `.ass` / `.ssa` auto-loaded by same name; CC toggle on the player page
- Three-source state sync: home page and player-page "Browse files" share library / local / network positions

### VR interaction
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
| **Settings** | Delay adjustment, skip no-action, idle easing, manual position, devices, firmware, activation, about |

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
- Speed: the speed button on the player controls cycles 1.0× / 1.25× / 1.5× / 2.0×, resetting to 1.0× on each new video.
- The playback-failure banner offers "Retry" to replay the last request; if no script auto-matches, you can browse and load one manually.
- Player bottom bar: **Home / Browse files / Video passthrough / Boost / Emergency stop / Idle easing / Linkage / Presets**.
- Top bar left: device pill (connect / disconnect during playback); right: passthrough / scene / CC.
- Format row: projection / stereo / load-script buttons; projection is re-detected for each new video.

### Script loading

Put a `.funscript` in the video's folder with the same name and it loads automatically. Also supported:

1. Set a directory as the **local script folder** on the "Local files" page (indexed recursively);
2. Configure a **remote script source** on the "Network sources" page (the script folder);
3. Pick a script manually in the player's "Browse files".

Priority is listed under "funscript / device sync" above. The network same-directory always wins over the local script folder for network videos.

### Device connection

Tap the device pill on the home / player page → choose a device to connect. Grant Bluetooth permission on first use; the device must be powered on and not occupied by another app.
Settings → Device info / Device advanced shows firmware, stroke range, speed limit, invert and OC.

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
- **How do I activate device linking?** Settings → Activation → paste your Afdian order ID / Ko-fi transaction ID → tap Claim. Owners of a ServeU (抚物) device activate free — add QQ `2831691505` to get your code.
- **Black or distorted picture**: switch projection / stereo format on the player page; playback failures show a red banner.
