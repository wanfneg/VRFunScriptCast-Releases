## 1.5.2 更新说明

## 修复

- **PICO 无法激活 / 点「领取」直接闪退**：验签模块用到了 Android 12+ 才有的接口，PICO 4（Android 10）一进入验签就崩。已修复，PICO 用户现在可以正常领取激活。
- **Android 13 机型面板可能崩溃**：创建面板虚拟屏时用了 Android 14 的接口，版本判断写宽了一档，已收紧。
- **领取 / 激活失败不再闪退**：任何异常都会在界面上给出提示，不再带走整个应用。

## 改进

- **更新说明更好读**：应用内更新弹窗现在会渲染标题 / 列表 / 加粗，支持**摇杆滚动**（原来内容会被截断），并按界面语言显示中文或英文说明。

## 安装说明

- 单包 `arm64-v8a`，`versionCode 10502 / versionName 1.5.2`，可从 1.5.1 直接覆盖升级。

<!--EN-->

## VRFunScriptCast 1.5.2

## Fixes

- **PICO could not activate / crashed when tapping Claim**: the license verifier used an Android 12+ API, so on PICO 4 (Android 10) it crashed the moment verification ran. Fixed — PICO users can claim and activate normally now.
- **Possible panel crash on Android 13**: creating panel virtual displays called an Android 14-only API behind an Android 13 version check; the guard is now correct.
- **No more crash when claim / activation fails**: any unexpected error is shown in the dialog instead of killing the app.

## Improvements

- **Readable update notes**: the in-app update dialog now renders headings / lists / bold text, scrolls with the thumbstick (it used to be cut off), and shows the notes in your UI language.

## Install

- Single `arm64-v8a` package, `versionCode 10502 / versionName 1.5.2`, upgrades in place over 1.5.1.
