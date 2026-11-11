# VRFunScriptCast v1.5.1 Release Notes

## New

- **Continuous playback**: when a video ends, the next one in the same folder plays automatically (can be turned off in Settings → skip panel, on by default).
- **Previous / Next episode**: two new buttons beside the ±10s seek keys on the player bar; they grey out when there is no adjacent video.
- **Playback speed**: a speed button on the player controls cycles 1.0× / 1.25× / 1.5× / 2.0×, resetting to 1.0× on each new video.
- **Retry on failure**: the playback error banner has a Retry button that replays the last request — no need to exit and re-enter.
- **Manual script loading**: if no matching script auto-loads, you can browse and load one manually.
- **Scroll memory**: the file browser remembers your scroll position per folder, and highlights the currently playing video.

## Improvements

- **Smoother panel scrolling**
- **Better UI interaction feedback**

## Fixes

- **Garbled names from network sources**
- **Distortion when zooming the VR view**
- **Scroll not working in the player's browse dialog**

## Activation

- This update adds **license verification** for **device linking** (BLE / TCode / Intiface). Playback, file browsing, network sources and everything else are unaffected and stay free.
- **ServeU (抚物) owners activate free**: if you already own a ServeU device, no license purchase is needed — contact the author on QQ `2831691505` to activate for free.
- Other users can activate in-headset via Settings → Activation → paste your order ID → Claim.

## Install

- Single `arm64-v8a` package, `versionCode 10501 / versionName 1.5.1`, upgrades in place over 1.5.0.
