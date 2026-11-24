<div align="center">
    <img src="docs/assets/banner.png" width="100%" alt="VRFunScriptCast">
</div>



<div align="center">

中文 | [English](README.en.md)

![Quest](https://img.shields.io/badge/Quest-3-8A2BE2)
![PICO](https://img.shields.io/badge/PICO-4-3DDC84)
![OpenXR](https://img.shields.io/badge/OpenXR-native-1E90FF)
![GitHub Repo stars](https://img.shields.io/github/stars/wanfneg/VRFunScriptCast-Releases)
![GitHub all releases](https://img.shields.io/github/downloads/wanfneg/VRFunScriptCast-Releases/total)

<p>Android + OpenXR 原生 VR 视频播放器（Quest / PICO）</p>

<img src="docs/assets/home-library-zh.jpg" width="96%" alt="主页媒体库" />
<br/>
<img src="docs/assets/player-zh.jpg" width="32%" alt="播放页" />
<img src="docs/assets/player-browse-zh.jpg" width="32%" alt="文件浏览" />
<img src="docs/assets/player-preset-zh.jpg" width="32%" alt="预设模式" />
<br/>
<img src="docs/assets/player-linkage-zh.jpg" width="32%" alt="联动控制" />
<img src="docs/assets/player-devices-zh.jpg" width="32%" alt="设备连接" />
<img src="docs/assets/player-mr-zh.jpg" width="32%" alt="视频透传" />
<br/>
</div>


<br/>

## 适配平台

- [x] Meta Quest 3（Android 14，已验收）
- [x] PICO 4 系列（已实机运行；机型 / 系统版本差异较大，遇异常请附机型与日志反馈）
- [x] arm64-v8a 单包，不分 Quest / Pico

## 功能

- [x] 视频播放与画面
  - [x] 投影格式：平面 / 经纬 180° / 经纬 360° / 鱼眼 180° / 鱼眼 190° / 镜头轮廓 200° / 220°，播放中随时切换
  - [x] 立体格式：上下 / 左右半宽 / 左右全宽 / 单视场
  - [x] VR 视角缩放：角向双射，抓握缩放不畸变
  - [x] 倍速七档 0.25× / 0.50× / 0.75× / 1.00× / 1.25× / 1.50× / 2.00×，连播、上 / 下一集、失败重试
  - [x] 进度条以 funscript 动作热力图呈现
- [x] 平面视频增强
  - [x] 光晕 / 氛围光双层光效，可分别开关与调强度；颜色跟随画面边缘实时取色，带地面接触阴影
  - [x] 2D 转 3D（实验性，仅平面投影 + 单目；头显本机逐帧估算深度生成视差，视频不上传、不依赖电脑；3D 弹窗可调「深度」「基准面」或重置；**默认关闭**，可在 设置 → 播放默认 开启自动启用）
  - [x] AV1 软件解码回退（arm64 / Android 13+，8-bit SDR；系统解码器不支持时启用）
- [x] 视频透传（MR）
  - [x] 绿 / 蓝 / 中性灰 / 浅灰色键抠像 + Alpha 透明通道 + 蒙版预览
  - [x] 自动识别当前帧主色，换片 / 重启不丢
- [x] 场景与透视
  - [x] 默认内置「柑橘果园晴空」；其余 7 个场景带预览、按需下载（Poly Haven CC0 HDRI；Quest 用 4K ASTC，其他设备回退 2K WebP），一键切换头显真实环境透视
- [x] 网络源与媒体库
  - [x] SMB / WebDAV / DLNA 局域网直连，无需拷贝
  - [x] SMB 真实枚举共享（含自定义共享）；WebDAV 支持 302 下载链；MP4 交错预读与高码率缓冲调优
  - [x] 媒体库快捷收藏、浏览位置自动记忆、三来源状态同步
  - [x] 本地 / 网络视频封面缩略图（铺满裁切、内存缓存）、目录排序与滚动位置记忆、逐文件续播记忆
  - [x] 外挂字幕 `.srt` / `.ass` / `.ssa` 同目录同名自动加载；MKV 内嵌字幕（PGS / ASS 等）可显示，CC 开关统一控制
- [x] FunScript 同步
  - [x] 脚本自动匹配（同目录同名 → 本地脚本文件夹 → 远程脚本文件夹）+ 手动点选
  - [x] 24 种波形预设 + RANDOM 循环随机 + BOOST 狂暴加速；行程 / 速度滑条实时可调
  - [x] 一键急停 / 一键爆发 / 待机缓动 / 联动控制
- [x] 设备联动（需激活许可证）
  - [x] BLE 蓝牙设备直连
  - [x] TCode / OSR 经典蓝牙 SPP 直连（OSR2 / SR6 / SSR1 等，v0.2 / v0.3 可选；单轴 / 4 轴 / 6 轴，多轴为测试功能）
  - [x] Intiface Central 桥（Buttplug，数百种设备）
  - [x] The Handy（FW4，BLE；运动为内测，连接后播放脚本即驱动；默认行程 0–100，自定义行程待验证）
  - [x] 行程范围 / 限速 / 反转 / 狂暴模式（OC）
- [x] 界面与交互
  - [x] 全局烟灰毛玻璃界面 + Noto Sans SC 字体；缓冲 / 快进提示固定在空间中的提示轨
  - [x] 设置 → 手柄操作：中英双语键位教程
  - [x] 激光指针 + 白点高亮，扳机点击，B / X 键返回
  - [x] 摇杆左右轻拨 ±10 秒跳转、按住持续快进快退；上下推动视角缩放
  - [x] grip 键按住拖动，自由移动 / 转动播放窗口

<br/>

## 下载

可以从 [Releases](https://github.com/wanfneg/VRFunScriptCast-Releases/releases/latest) 下载，或从 [SideQuest](https://sidequestvr.com/app/63810) 安装。
单一 `arm64` APK，同签名直接覆盖升级。当前 **v1.6.1**（约 73 MB；默认 1 个场景，其余 7 个按需下载）；完整中英更新说明见 Releases。

- **Discord（反馈 / 测试交流）**：https://discord.com/invite/fXKaVbn4NF

详细用法见 **[使用手册](docs/user-guide.md)**（已知限制 / 功能总览 / 安装 / 快速上手 / 常见问题）。

<br/>

## 赞助与授权

播放、文件浏览、网络源等**全部功能永久免费**。
仅「设备联动」（BLE / The Handy / TCode / Intiface）需要一次性许可证：**Lifetime，一码一机，永久有效**。

| 地区 | 平台 | 支付方式 | 价格 | 链接 |
|---|---|---|---|---|
| 中国大陆 | 爱发电 | 支付宝 / 微信 | ¥30 | https://afdian.com/item/92b5f30edd1c11f1ad7d52540025c377 |
| 其他地区 | Ko-fi | PayPal / 信用卡 | $9.99 | https://ko-fi.com/s/4bcd6114c5 |

**激活步骤**：头显内「设置 → 激活」→ 粘贴订单号 / 交易号 → 点「领取」，自动完成激活。
换设备或恢复出厂设置后请提交订单号申请换绑。

**抚物（ServeU）设备用户**：已经购买抚物设备的用户可**免费激活**——打开设备电源并靠近头显，在「设置 → 激活 → 抚物设备免费激活」点一下即可自动完成，无需订单号。`2831691505`（作者 QQ）作为兜底联系渠道。

<br/>

## 声明

本项目由个人出于兴趣开发；不提供、不索引、不包含任何盗版或破解内容。
请勿倒卖安装包，搬运请注明出处。

感谢使用

<br/>

## 致谢

- [Khronos OpenXR-SDK](https://github.com/KhronosGroup/OpenXR-SDK)（Apache-2.0）
- [Media3 / ExoPlayer](https://github.com/androidx/media)
- Kotlin / Jetpack Compose
- 等等

<br/>
<br/>
<br/>

## Star History

<a href="https://star-history.com/#wanfneg/VRFunScriptCast-Releases&Date">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=wanfneg/VRFunScriptCast-Releases&type=Date&theme=dark" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=wanfneg/VRFunScriptCast-Releases&type=Date" />
   <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=wanfneg/VRFunScriptCast-Releases&type=Date" />
 </picture>
</a>
