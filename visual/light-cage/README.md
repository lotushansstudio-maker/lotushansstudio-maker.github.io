# 光笼 · Light Cage

几万个光点组成的数学雕塑，住在一个发光的线框立方体里。你可以把它托在掌心，用双手把笼子撑开，让粒子散成洛伦兹流，然后握拳让它们汇聚成下一件雕塑。

A particle sculpture lives inside a glowing wireframe cube. Hold it in your palm, pull the cage open with both hands, watch it scatter into a Lorenz flow, then make a fist to collapse it into the next shape.

## 四幕（全靠手势自然推进，没有切换按钮）

1. **掌心**：摊开一只手，水母浮在掌心上方，一张一缩地呼吸
2. **撑开**：双手拇指和食指就是笼子前面的四个顶点，拉大笼子，雕塑散开
3. **流动**：粒子沿洛伦兹吸引子奔流；伸出食指能拨开一个空洞；笼子被手拉歪，里面的粒子也一起变形
4. **换形**：握拳，粒子向中心汇聚；松开，重组成下一件雕塑

五件雕塑都由公式生成：水母、洛伦兹吸引子、百合、三叶结、黄金角球。左下角实时显示当前雕塑的公式和粒子数。

## 玩法

| 操作 | 电脑 | 手机 | 摄像头 |
|---|---|---|---|
| 散开 / 凝聚 | 点一下（或空格） | 点一下 | 双手撑大 / 合拢 |
| 换形 | 长按后松开（或 N、→） | 长按后松开 | 握拳后松开 |
| 转动光笼 | 拖动 | 拖动 | 双手倾斜 |
| 缩放 | 滚轮 | 双指 | 双手距离 |
| 拨开粒子 | 鼠标移过 | 手指按住移动 | 伸出食指 |
| 单手 | — | — | 捏住拇指和食指拖出一个笼子；摊开手掌托住雕塑 |

7 秒没人操作会自动演示：散开 → 流动 → 汇聚 → 换形。右上角可切换中英文。

## 灵感来源

- Instagram [@wxll.hx](https://www.instagram.com/wxll.hx/) 的两段 TouchDesigner 手势作品：掌心托着物体散成粒子云；双手撑开 3D 线框立方体，笼内是粒子雕塑，握拳切换
- 本作从头用网页重写，雕塑不用任何外部模型，全部是数学曲面 / 方程

## 技术

- 单文件 `index.html`，不依赖任何库；WebGL 点精灵 + 叠加发光（additive blending）
- 粒子在光笼的局部坐标 [-1,1]³ 里运动，再用笼子 8 个顶点做三线性插值映射到屏幕，所以笼子变形时雕塑跟着变形
- 散开时每个粒子按洛伦兹方程 ẋ=σ(y−x), ẏ=x(ρ−z)−y, ż=xy−βz（σ=10, ρ=28, β=8/3）积分，被吸引子“捕获”
- 凝聚用阻尼弹簧，每个粒子有不同延迟，形成“流回去”的光带
- 手势：MediaPipe Hand Landmarker（最多两只手，npmmirror 镜像优先，失败换同站 `/ascii-xmas-tree/mp/`，模型校验 SHA-256）
- 摄像头画面压暗去饱和做背景，让光成为主角
- 电脑 36,000 个粒子，手机 16,000 个

## 怎么改成自己的

- 换颜色：改 `shapeColor()` 和 `SHAPE_GLOW`
- 加一件新雕塑：在 `home()` 里加一个分支（输入 a,b,c∈[0,1] 和时间 T，输出坐标），再在 `SHAPES_I18` 和 `FORMULA` 里加名字和公式
- 改流动方程：`frame()` 里 `mode === 'free'` 的那段，换成 Rössler、Aizawa 等其他吸引子

## 发布到 GitHub Pages

把 `index.html` 放进个人主页仓库 `visual/light-cage/` 目录，推送后访问
`https://lotushansstudio-maker.github.io/visual/light-cage/`（摄像头需要 https，Pages 默认就是）。
