# 《熄灯人》The Wickless

暗黑国风 · 俯视角动作 Roguelite。**生命 = 光源 = 视野 = 暴露度**，四者绑在同一根蜡烛上。

- 越亮 → 越能打、越看得清，但也越被盯上
- 越暗 → 安全但近乎失明，敌人在暗处等你熄火
- 击杀不直接回血，掉落**蜡屑**，必须走出去捡

## 目录

| 路径 | 说明 |
|---|---|
| `docs/GDD-暗黑类游戏-大纲.md` | 整体大纲：TapTap 上架路径、品类、核心循环、美术与商业化 |
| `prototype/wickless.html` | 可玩原型，单文件 HTML5 Canvas，无依赖 |
| `prototype/tests/` | 自动化测试页（需通过 HTTP 打开，见下） |

## 跑起来

```bash
cd prototype
python3 -m http.server 12000
```

浏览器打开 `http://127.0.0.1:12000/wickless.html`。

**操作**：`WASD` / 方向键移动 · 鼠标瞄准 · `J` 或左键挥砍 · `K` 爆燃 · `Shift` 剪灯芯（省蜡但视野骤减）· `R` 重开

## 测试

测试页通过 iframe 加载原型并驱动其 `window.__wickless` 调试钩子，所以必须用 HTTP 打开（`file://` 会被同源策略挡住）。

| 页面 | 内容 |
|---|---|
| `tests/_selftest.html` | 渲染冒烟测试：画面非黑、无运行时异常 |
| `tests/_logictest.html` | 26 项行为断言：蜡量 / 视野 / 剪芯 / 掉落 / 拾取 / 敌人 AI / 暗风 |
| `tests/_probe.html` | 机器人长跑探针：完美瞄准 vs 普通 vs 手残，观察蜡量曲线与死亡时间 |
| `tests/_bottest.html` | 贪心 vs 保守两种策略对比 |

`_logictest.html` 全 PASS 时页面标题为 `ALLPASS`，可直接用脚本判定。

## 当前状态

原型阶段，手感与平衡仍在调。已知问题：完美走位下难度爬升偏慢，正在通过敌人构成与资源曲线收敛。
