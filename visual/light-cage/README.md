# 光笼 · Light Cage

几万个光点组成的数学雕塑，住在一个发光的线框立方体里。你可以把它托在掌心，用双手把笼子撑开，让粒子散成洛伦兹流，然后握拳让它们汇聚成下一件雕塑。

A particle sculpture lives inside a glowing wireframe cube. Hold it in your palm, pull the cage open with both hands, watch it scatter into a Lorenz flow, then make a fist to collapse it into the next shape.

## 玩法（v2：按原作逐帧对齐）

- **托笼子的手**（画面左边那只，张开）：发光的白色线框立方体托在掌心，跟着手移动、缩放；手倾斜、手掌转向时，立方体跟着转
- **控制手**（右边那只）：**握拳** = 雕塑凝聚成形；**张开** = 炸散成一团团纤维，在笼子里沿 ABC 流翻卷；每次再握拳，凝聚成下一件雕塑
- **只用一只手**：雕塑托在掌心；握拳汇聚、张开换下一件；快速移动手，雕塑会被甩成白色点云拖在后面，停下来再凝回原样
- 摄像头画面原样显示（不压暗），雕塑和纤维用普通透明叠加，所以深色、浅色背景都看得清

五件雕塑都由公式生成：水母、洛伦兹吸引子、百合、三叶结、黄金角球。左下角实时显示当前雕塑的公式；炸散时显示 ABC 流方程。

| 操作 | 电脑 | 手机 | 摄像头 |
|---|---|---|---|
| 炸散 / 凝聚成下一件 | 点一下（或空格） | 点一下 | 右手张开 / 握拳 |
| 转动光笼 | 拖动 | 拖动 | 左手倾斜、转动 |
| 缩放 | 滚轮 | 双指 | 左手靠近 / 远离镜头 |
| 汇聚 | 长按 | 长按 | 单手握拳 |
| 拨开粒子 | 鼠标移过 | 手指按住移动 | — |

7 秒没人操作会自动演示。右上角可切换中英文。

## 灵感来源

- Instagram [@wxll.hx](https://www.instagram.com/wxll.hx/) 的两段 TouchDesigner 手势作品：一只手托着白色线框立方体，另一只手张开让里面的模型炸成纤维、握拳换下一个模型；掌心托物、移动时散成白色点云
- 本作从头用网页重写，雕塑不用任何外部模型，全部是数学曲面 / 方程

## 技术

- 单文件 `index.html`，不依赖任何库；WebGL 点精灵 + 叠加发光（additive blending）
- 粒子在立方体的局部坐标 [-1,1]³ 里运动，跟着立方体一起转；凝聚时目标是屏幕空间里直立的雕塑
- 炸散时每个粒子沿 ABC 流（Arnold–Beltrami–Childress，u=A sin z+C cos y, v=B sin x+A cos z, w=C sin y+B cos x）运动，最近 12–16 帧的轨迹画成纤维，看起来像一团团发丝
- 立方体是真 3D：中心、大小、三个转角由手的关键点算出（掌长 × 1.6；手掌法向量 → 转向），透视投影
- 凝聚用阻尼弹簧，每个粒子有不同延迟，形成“流回去”的光带
- 手势：MediaPipe Hand Landmarker（最多两只手，npmmirror 镜像优先，失败换同站 `/ascii-xmas-tree/mp/`，模型校验 SHA-256）
- 电脑 30,000 个粒子（其中 9,000 根纤维），手机 14,000 个

## 怎么改成自己的

- 换颜色：改 `shapeColor()` 和 `SHAPE_GLOW`
- 加一件新雕塑：在 `home()` 里加一个分支（输入 a,b,c∈[0,1] 和时间 T，输出坐标），再在 `SHAPES_I18` 和 `FORMULA` 里加名字和公式
- 改炸散的流场：`frame()` 里 `mode === 'free'` 的那段，换成其他向量场（比如洛伦兹、Aizawa）

## 发布到 GitHub Pages

把 `index.html` 放进个人主页仓库 `visual/light-cage/` 目录，推送后访问
`https://lotushansstudio-maker.github.io/visual/light-cage/`（摄像头需要 https，Pages 默认就是）。
