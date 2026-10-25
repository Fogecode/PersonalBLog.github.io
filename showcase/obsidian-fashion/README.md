# obsidian-fashion · Obsidian 时装柜

![obsidian-fashion — Themes fashioned from the web, worn in two ways](images/poster.png)

> **Themes *fashioned* from the web, *worn* in two ways (dark & light).**
> 从万千网页 UI 风格中裁制而成的 Obsidian 主题——每件外套，两面穿。

一间持续上新的 Obsidian 时装柜：每件主题都内置深、浅两套配色，随 Obsidian
「基础模式」**无缝换装**（手动切深浅，或开「自动跟随系统」日出日落自动换）。
macOS 毛玻璃、赛博朋克霓虹、HUD 机甲、故障艺术、Nord、Solarized、GitHub、
杂志、终端……总有一件合身。同款主题也穿在
[Typeset](https://github.com/Fogecode/Typeset) 导出的网页上——笔记穿什么，
导出就穿什么。

当前版本 **v2.0.1**（2026-10-24）。作者作品家族：[Typeset](https://github.com/Fogecode/Typeset)（排版导出）×
obsidian-fashion（穿衣打扮）。

## 主题图册

整体观感见顶部海报——每张卡片的深/浅两半，就是用该主题两种模式的真实配色画的。

### 深色基因（浅色为对侧配色）

| 主题 | 深色面 | 浅色面 |
| --- | --- | --- |
| macOS Vibrancy | 三层深灰 + 侧栏毛玻璃 | macOS 官方浅灰系毛玻璃 |
| Cyberpunk Neon | 近黑底 + 青色霓虹 + 品红标签 | 冰蓝日霓虹 |
| Cyber Anime | 深紫 HUD：角框 callout + 六边形网格 | 淡紫日间 HUD |
| Glitch Art | 纯黑 + CMY + 标题 RGB 分离 + 全等宽 | 复印纸风白底油墨色 |
| Terminal Phosphor | 磷光绿终端：`##` 提示符 + 闪烁光标 | 纸带绿终端 |
| Nord Dark | Nord 官方夜读配色 | Nord Light（官方） |

### 浅色基因（深色为对侧配色）

| 主题 | 浅色面 | 深色面 |
| --- | --- | --- |
| Paper | 暖米白印刷：衬线正文 + 章节短线 | 夜航书：暖褐纸 + 亮赭 |
| Neo-Brutalist | 酸黄 + 黑框 + 硬阴影 + 零圆角 | 黑底 + 白框 + 酸黄硬影 |
| Swiss | 白底红点缀 + 发丝线网格 | 深灰 + 亮红 |
| Solarized Light | 经典 Solarized Light | Solarized Dark（官方） |
| Magazine | 米白刊物：居中报头 + 首字下沉 | 午夜刊：暖黑 + 亮牛血红 |
| GitHub | Primer 文档风 | GitHub Dark（官方） |

## 安装

1. 把 `themes/` 下想要的**整个主题文件夹**复制到你的仓库：
   `<vault>/.obsidian/themes/<主题名>/`
2. Obsidian 里 `Ctrl+P` → `Reload app without saving`
3. `设置 → 外观 → 主题` 选择；想切深浅就切「基础模式」（或开自动跟随系统）

卸载：切回默认主题即不生效；彻底删除 = 删对应主题文件夹。

## 主题里的可玩开关

每套 `theme.css` 顶部都有注释化的「特效开关」：

- **静态档**：所有 `--fx-*` 设 `none`（零特效最省电）
- **轻特效（默认）**：hover/焦点发光、扫描线等，无常驻动画
- **全特效**：按注释里的预设值放开（编辑区常驻扫描线等）

Terminal 的 `##` 提示符前缀、Magazine 的首字下沉均有独立关闭说明。

## 版本史（要点）

| 版本 | 内容 |
| --- | --- |
| v2.0.1 | 对侧模式真机验收修复：表头错色 ×6、Glitch 浅色重影、Solarized Dark 重调 |
| v2.0.0 | 双主题：12 套全部配齐深浅两套配色，随基础模式无缝切换 |
| v1.3.0 | Swiss 表格/代码框叠加态；表格作用域统一 `.markdown-rendered` |
| v1.2.x | 以本机 Obsidian app.css 为真值的全量校对（死变量清理 / WCAG 对比度） |
| v1.0–1.1 | 两批共 12 套主题制作、明暗自适应、参考图版式迭代 |

## 工程说明

- 纯 CSS 主题（无 JS、零构建、零网络行为），变量层 + 母题层 + 特效层三段式。
- 质量链：官方变量名审计（对照本机 Obsidian app.css）→ 双调色板 WCAG 对比度审计 →
  DOM 骨架渲染断言（含深浅翻转）→ 装机哈希校验。
- 血统：6 套提取自自家 [Typeset](https://github.com/Fogecode/Typeset) 导出器的内置主题
  （tokens 忠实移植），4 套译自 [luckymaomi 风格库](https://luckymaomi.github.io/ui/styles/)，
  对侧配色 Nord/GitHub/Solarized/macOS 采用官方配色。

## License

[MIT](LICENSE)

## 致谢与素材来源（Attribution）

本仓库的全部 CSS 为原创编写（Obsidian 官方 CSS 变量接口之上的自研实现），
以下素材在**设计灵感或调色板层面**被引用（设计风格与色彩值不属于版权客体，
所引开源调色板项目本身亦为 MIT）：

- [luckymaomi UI 风格库](https://luckymaomi.github.io/ui/styles/) —
  macOS Vibrancy / Cyberpunk Neon / Cyber Anime / Glitch Art 四套的风格灵感来源
- [Nord](https://github.com/arcticicestudio/nord)（MIT）— Nord Dark / Nord Light 调色板
- [Solarized](https://github.com/altercation/solarized)（MIT）— Solarized Light / Dark 调色板
- [GitHub Primer](https://github.com/primer/css)（MIT）— GitHub Light / Dark 调色板
- [Obsidian](https://obsidian.md) — 主题化所依赖的公开 CSS 变量与 DOM 接口
- [Typeset](https://github.com/Fogecode/Typeset)（本项目作者自研，MIT）—
  8 套主题的初代血统（导出器内置主题的忠实移植与再创作）
