# NewMarsHeartBeat

**在线访问地址**：https://SamZebrado.github.io/NewMarsHeartBeat/

## 项目简介
这是一款由 SamZebrado 与豆包 AI 自主开发的心率数据可视化网页，可接收 HeartRateMonitorMobile 开源项目推送的 WebSocket 心率数据并实时展示；支持在 Android 设备上通过 Floating Apps 实现简洁的悬浮组件展示效果，完整开源可自由部署。

## 开发小故事
我个人非常喜欢小米，这段经历只是分享设备适配的小插曲，完全没有任何负面意思～

最初我想实现一个方便的心跳数据展示方案，过程中尝试了多款小米/红米设备：先是用红米 Watch 5 连接小米平板 7 Pro，却一直没能稳定连接；后来把手表绑定到 Redmi K50，能配对但又不显示心率数据。最后抱着试一试的心态，用 Redmi K30Pro 作为服务端（仅通过 BLE 连接手表，不绑定），平板 7 Pro 作为客户端，结合自己开发的这个网页和 Floating Apps，居然完美实现了悬浮展示的效果！

正是因为喜欢小米产品的设计和体验，才会折腾出这个有趣的适配方案，也感谢 HeartRateMonitorMobile 和 Floating Apps 让这个想法落地～

## 核心功能
- 💓 实时可视化：接收 WebSocket 心率数据，通过折线图动态展示心率波动趋势
- 🪟 悬浮展示：适配 Android 平台 Floating Apps，实现简洁的心率悬浮组件效果
- 🎨 双击自定义外观：支持通过双击不同区域调节界面元素比例与间距，实时预览并保存设置
- 🌐 **双语切换**：支持中文和英文界面，**长按心形图标 5 秒钟**即可切换语言
- 🔌 数据对接：无缝对接 HeartRateMonitorMobile 的 WebSocket 数据推送协议
- 🚀 轻量部署：可一键部署至 GitHub Pages，无需额外服务器支撑
- 🛠️ 易定制：代码结构清晰，支持自定义可视化样式与数据更新频率

## 双语切换功能

### 使用方法
- **长按心形图标 5 秒钟**即可在中文和英文界面之间切换
- 首次访问时，页面会根据浏览器的语言设置自动选择中文或英文
- 语言偏好会保存在本地（localStorage），下次访问时会自动使用上次选择的语言

### 技术实现
- 使用 `localStorage` 保存用户选择的语言偏好
- 首次加载时自动检测浏览器语言（`navigator.languages` / `navigator.language`）
- 长按检测：使用 Pointer Events（已避免 pointerleave/lostpointercapture 误取消）（`pointerdown`/`pointerup`/`pointercancel`/`pointermove`）统一处理鼠标与触摸输入，启动 5 秒定时器
- 如果用户在 5 秒内释放，则判定为普通点击，触发双击调节面板
- 如果长按达到 5 秒，则触发语言切换

## 外观自定义指南
通过双击界面不同区域，可打开对应的调节面板，所有设置支持实时预览、恢复默认与本地保存：

| 双击区域               | 调节功能                     | 调节范围                  |
|------------------------|------------------------------|---------------------------|
| 心跳图标（**双击**）   | 图标相对于数字的大小比例     | 0.5x - 6x                 |
| 心率数字（红色）       | WebSocket 地址配置           | 自定义输入                |
| 单位文字（灰色"次/分钟"） | 单位文字相对于数字的大小比例 | 0.1x - 2x                 |
| 图标与数字之间的空隙   | 图标与数字的垂直间距         | 0em - 2em（0 为无空隙）  |
| 数字与单位之间的空隙   | 数字与单位的垂直间距         | 0em - 2em（0 为无空隙）  |

> ⚠️ **注意**：长按心形图标 5 秒会切换语言，如果只想双击调节比例，请确保按压时间少于 5 秒。

## 快速开始
### 本地运行
1. 克隆本仓库到本地
```bash
git clone https://github.com/SamZebrado/NewMarsHeartBeat.git
```
2. 部署 HeartRateMonitorMobile 开源项目并开启 WebSocket 数据推送功能：
```bash
git clone https://github.com/ccc007ccc/HeartRateMonitorMobile
```
3. 按照 HeartRateMonitorMobile 文档配置 WebSocket 服务，确保数据可正常推送
4. 进入本项目目录，打开 `index.html`，配置 WebSocket 服务地址即可实时显示心率

### 部署到 GitHub Pages
1. 将本项目代码推送至你的 GitHub 公开仓库
2. 进入仓库设置 → Pages，选择部署分支（如 main）与根目录
3. 保存后等待自动部署，获取在线访问地址
4. 在 Android 设备上通过 Floating Apps 打开该地址，即可显示悬浮心率组件

> ⚠️ **连接说明**：GitHub Pages 使用 HTTPS。部分浏览器或 WebView 可能会拦截 HTTPS 页面中的 `ws://` 局域网 WebSocket 连接。如果连接失败，可尝试用本地文件、本地 HTTP 服务打开页面，或将心率 WebSocket 服务配置为 `wss://`。

## 开源引用与致谢
### 核心开源依赖
- 心率数据推送源：[HeartRateMonitorMobile](https://github.com/ccc007ccc/HeartRateMonitorMobile)（@ccc007ccc）—— 为本项目提供 WebSocket 格式的心跳数据源，感谢作者开源这一优秀的 BLE 心率监测应用
- 悬浮窗口工具：Floating Apps（Floating Widgets）—— 支持在 Android 设备上实现简洁的心率悬浮展示效果，感谢开发团队的优秀工具
- 数据可视化组件：[Chart.js](https://github.com/chartjs/Chart.js) —— 提供轻量高效的心率折线图展示能力

## 免责声明
- 本项目为 SamZebrado 的个人非商业项目，与小米公司、NASA、ESA 等任何组织无官方关联
- 项目中提及的小米/红米设备仅为个人使用经历分享，出于对小米产品的喜爱，无任何负面评价或恶意

## 许可证
本项目基于 Apache License 2.0 开源，详见 [LICENSE](LICENSE) 文件。
- 依赖组件 Chart.js：MIT License（https://github.com/chartjs/Chart.js）
- 心跳数据对接源 HeartRateMonitorMobile：请查看其仓库许可证（https://github.com/ccc007ccc/HeartRateMonitorMobile）


---

# NewMarsHeartBeat

## Project Overview
This is an independently developed heart rate data visualization webpage by SamZebrado and Doubao AI, which receives real-time WebSocket heart rate data pushed by the open-source HeartRateMonitorMobile project; supports clean floating widget display via Floating Apps on Android devices, fully open-source and free to deploy.

## The Story Behind This Project
I personally really like Xiaomi. This story is just a small note about device compatibility — no criticism intended.

Initially, I wanted to build a convenient heart rate display solution, and tried several Xiaomi/Redmi devices during the process: first, I tried connecting Redmi Watch 5 to Xiaomi Pad 7 Pro, but never got a stable connection; then I bound the watch to Redmi K50, it could pair but didn't show any heart rate data. Finally, with a try-it-out mindset, I used Redmi K30Pro as the server (only connecting to the watch via BLE, not binding), Pad 7 Pro as the client, combined with this webpage I developed and Floating Apps, and it actually worked beautifully as a floating display.

This little workaround came from my fondness for Xiaomi products and the urge to keep tinkering. Thanks also to HeartRateMonitorMobile and Floating Apps for making the idea possible.

## Core Features
- 💓 Real-time visualization: Receive WebSocket heart rate data and dynamically display heart rate fluctuation trends via line charts
- 🪟 Floating display: Designed to work with Floating Apps on Android for a clean floating heart rate widget
- 🎨 Double-click to customize appearance: Adjust element sizes and spacing by double-clicking different areas, with real-time preview and saved settings
- 🌐 **Bilingual Support**: Supports Chinese and English; **long-press the heart icon for 5 seconds** to switch languages
- 🔌 Data integration: Integrates with the WebSocket data streaming protocol of HeartRateMonitorMobile
- 🚀 Lightweight deployment: One-click deployment to GitHub Pages without additional server support
- 🛠️ Easy customization: Clear code structure, with support for custom visualization styles and data update frequency

## Bilingual Switching Feature

### How to Use
- **Long-press the heart icon for 5 seconds** to switch between Chinese and English interfaces
- On first visit, the page automatically selects Chinese or English based on your browser's language settings
- Language preference is saved locally (localStorage), so on next visit it will automatically use your last selected language

### Technical Implementation
- Uses `localStorage` to save the user's language preference
- Automatically detects browser language on first load (`navigator.languages` / `navigator.language`)
- Long-press detection: Uses Pointer Events（已避免 pointerleave/lostpointercapture 误取消） (`pointerdown`/`pointerup`/`pointercancel`/`pointermove`) to handle mouse and touch input consistently, then starts a 5-second timer
- If the user releases within 5 seconds, it's treated as a regular click/tap (double-click to open adjustment panel)
- If the long press reaches 5 seconds, it triggers language switching

## Appearance Customization Guide
By double-clicking different areas of the interface, you can open the corresponding adjustment panel. All settings support real-time preview, reset-to-default and local saving:

| Double-click Area               | Adjustment Function                     | Adjustment Range                  |
|----------------------------------|-----------------------------------------|-----------------------------------|
| Heart icon (**double-click**)    | Size ratio of icon relative to number   | 0.5x - 6x                         |
| Heart rate number (red)         | WebSocket address configuration         | Custom input                      |
| Unit text (gray "BPM")          | Size ratio of unit text relative to number | 0.1x - 2x                     |
| Gap between icon and number      | Vertical spacing between icon and number | 0em - 2em (0 = no gap)        |
| Gap between number and unit      | Vertical spacing between number and unit | 0em - 2em (0 = no gap)        |

> ⚠️ **Note**: Long-pressing the heart icon for 5 seconds will switch language. If you only want to double-click to adjust the ratio, please make sure the press duration is less than 5 seconds.

## Quick Start
### Local Run
1. Clone this repository to your local machine
```bash
git clone https://github.com/SamZebrado/NewMarsHeartBeat.git
```
2. Deploy the open-source HeartRateMonitorMobile project and enable WebSocket data streaming:
```bash
git clone https://github.com/ccc007ccc/HeartRateMonitorMobile
```
3. Configure the WebSocket service according to the HeartRateMonitorMobile documentation to ensure data can be pushed normally
4. Enter the project directory, open `index.html`, and configure the WebSocket service address to display heart rate in real time

### Deploy to GitHub Pages
1. Push the project code to your public GitHub repository
2. Go to Repository Settings → Pages, select the deployment branch (e.g., main) and root directory
3. Wait for automatic deployment after saving, and get the online access address
4. Open the address via Floating Apps on your Android device to display the floating heart rate widget

> ⚠️ **Connection note**: GitHub Pages is served over HTTPS. Some browsers or WebViews may block `ws://` local-network WebSocket connections from an HTTPS page. If the connection fails, try opening the page as a local file, serving it over local HTTP, or using a `wss://` WebSocket endpoint.

## Open Source Citation & Acknowledgements
### Core Open Source Dependencies
- Heart rate data source: [HeartRateMonitorMobile](https://github.com/ccc007ccc/HeartRateMonitorMobile) (@ccc007ccc) —— Provides WebSocket-format heart rate data source for this project, thanks to the author for open-sourcing this excellent BLE heart rate monitoring app
- Floating window tool: Floating Apps (Floating Widgets) —— Enables clean floating display of heart rate on Android devices, thanks to the development team for this great tool
- Data visualization component: [Chart.js](https://github.com/chartjs/Chart.js) —— Provides lightweight and efficient line chart display for heart rate

## Disclaimer
- This is a personal non-commercial project by SamZebrado, with no official association with Xiaomi Corporation, NASA, ESA, or any other organization
- The Xiaomi/Redmi devices mentioned in the project are only for personal use experience sharing, out of love for Xiaomi products, without any negative comments or malice

## License
This project is open source under the Apache License 2.0, see the [LICENSE](LICENSE) file for details.
- Dependent component Chart.js: MIT License (https://github.com/chartjs/Chart.js)
- Heart rate data source HeartRateMonitorMobile: Please check its repository license (https://github.com/ccc007ccc/HeartRateMonitorMobile)
