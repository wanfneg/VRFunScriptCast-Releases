# VRFunScriptCast

本项目由我个人借助 AI 工具开发。个人精力的付出、AI 工具的使用都有成本，而项目**免费**提供给大家使用。

欢迎大家体验，并提出 **BUG 反馈、功能需求、优化建议**。也欢迎大家投喂白饭给大肥鱼，助力项目开发。

<p align="center">
  <img src="docs/sponsor/meme.jpg" alt="梗图" width="420">
</p>

<p align="center">
  <img src="docs/sponsor/wechat.png" alt="微信赞助" width="300">
  &nbsp;&nbsp;&nbsp;
  <img src="docs/sponsor/alipay.jpg" alt="支付宝赞助" width="300">
</p>

**沟通渠道**：QQ `2831691505`

---

**VR 版 FunScriptCast** —— Meta Quest / Pico 双平台 VR 媒体播放器与 funscript 同步应用。

戴上头显即可浏览本地与局域网媒体库、观看 2D/全景/3D 视频，并让实体玩具设备（ServeU、Vorze 等遵循官方/第三方协议的产品）按 funscript 与画面精确同步。

> 本仓库是**安装包发布仓库**（仅 APK，不含源码，源码仓库为私有）。
> 请在 [Releases](https://github.com/wanfneg/VRFunScriptCast-Releases/releases) 页面下载最新版本。


## 赞助与支持

## 主要功能

- **视频播放**：本地文件 + 网络源（DLNA / SMB / WebDAV）统一走 ExoPlayer 管线（硬解、缓冲重试、拖动）
- **投影与立体**：2D 平面窗口、全景 180°/220°/微鱼眼；上下 / 左右 / 半 SBS，运行时切换
- **视频透传（MR 抠像）**：色键抠像（绿/蓝/灰预设 + 自动识色）、Packed-Alpha 3×2 蒙版直通、蒙版预览
- **funscript 同步**：脚本模式（官方时间轴语义、延迟调整、跳过无动作段）、预设模式、快捷动作、行程/限速/反转/狂暴
- **设备管理**：BLE 扫描与直连、设备信息、WiFi 列表、OTA 固件更新
- **媒体库**：快捷收藏、文件浏览与浏览记忆、脚本自动匹配（同级同名 → 本地脚本文件夹 → 网络源同目录 → 远程脚本源索引）

## 支持平台

| 平台 | 安装包 |
|---|---|
| Meta Quest 3 | `VRFunScriptCast-Meta.apk` |
| Pico | `VRFunScriptCast-Pico.apk` |
