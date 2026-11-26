# 扫描取景 · Scan Frame

用手撑出一个取景框，框里的世界变成发光的扫描线；松手，这一帧定格成一张贴纸，越叠越像拼贴。
Frame any part of the world with your hands and it turns into glowing scanlines. Release to freeze it into a sticker.

## 玩法
- **鼠标 / 单指**：拖出一个框，松手定格
- **手机双指**：两根手指撑开对角，抬起手指定格
- **摄像头**：举起手，取景框跟着手走；拇指碰一下食指就定格。双手时，两只手撑出框的对角
- 不用手动选滤镜：每定格一次，按原作顺序自动换下一种（线描 → 色阶 → 四叉树 → 晒蓝 → 扫描线 → 循环）
- 画面和原作一致：框外是原画面，取景框只有一圈细白线，贴纸没有边框；第一次定格后界面自动隐去
- 键盘 `Z` 撤销，`X` 清空，`S` 保存，`C` 摄像头
- 没有操作时，会有一个取景框自己慢慢游走做演示
- 「照片」按钮可以用自己的照片当素材

## 五种滤镜
1. **扫描线（主角）**：`y′ = y + k·L(x,y)`，每条横线按亮度被推高，形成等高线浮雕和摩尔纹；有残影、暗处星点和一道下扫的光带
2. 线描：Sobel 边缘 `|∇I| = √(Gx²+Gy²)` + 暗部排线
3. 色阶：亮度切四档，黄色版错位，像丝网印刷
4. 四叉树：格子方差 `σ² > τ` 就一分为四
5. 晒蓝：阈值 + 有序抖动

## 来源
灵感来自 Instagram 创作者 @wxll.hx 的 TouchDesigner 手势取景框作品（2026-11 Lotus 分享）。代码从头写，未使用原作素材。

## 技术
- 单文件 `index.html`，WebGL1 着色器做全部滤镜、辉光；无外部库
- 摄像头手势：MediaPipe Hands（双手）；人像分割：MediaPipe selfie_segmenter，让人发光、背景压暗
- 运行库走 npmmirror，模型走国内镜像，失败自动换 GitHub 本站文件，下载后校验 SHA-256
- `selfie_segmenter.tflite`（约 250KB，Apache-2.0，与 Google 官方文件一致）需和 index.html 放在同一目录
- 无摄像头时素材是程序化光滑雕塑（光线步进渲染）

## 发布到 GitHub Pages
线上地址：https://lotushansstudio-maker.github.io/visual/scan-frame/ 。`index.html` 和 `selfie_segmenter.tflite` 放在同一目录即可。
