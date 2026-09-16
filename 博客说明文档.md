# 📘 ThersummerBlog 博客说明文档

> 本文档介绍这个博客项目是什么、怎么跑起来、怎么写文章、怎么部署，以及日常维护需要注意什么。

---

## 一、博客简介

**ThesummerBlog** 是一个基于 [Docsify](https://docsify.js.org/) 搭建的个人静态博客，托管在 GitHub Pages 上（仓库：`Fogecode/PersonalBLog.github.io`，用户主页站点，部署后直接挂在域名根路径）。

- 🚩 内容方向：个人学习记录、醒狮社区项目文档
- 📝 写作格式：纯 Markdown，写好 `.md` 文件加入侧边栏即可发布
- 🎨 个性化：自定义毛玻璃导航栏 + 五主题一键切换滑块

Docsify 的特点是**无需构建**：不做 markdown 预编译，浏览器运行时通过 AJAX 拉取 `.md` 文件实时渲染，所以整个项目就是"一个 `index.html` + 一堆 markdown"。

---

## 二、特色功能

### 1. 封面页（`_coverpage.md`）
打开网站首先显示封面（头像、标语、GitHub / Get Started 按钮）。`index.html` 中配置了 `onlyCover: true`，首页只展示封面。

### 2. 自定义顶部导航栏
`index.html` 内置毛玻璃导航栏（Logo + "ThesummerBlog" 渐变文字 + 🏠 首页链接）。Docsify 原生导航（`_navbar.md`）被 `.app-nav { display: none }` 隐藏，作为备用方案保留。

### 3. 毛玻璃主题切换滑块（右上角）
五个主题一键切换，选中结果存入 localStorage，刷新后保持：

| 图标 | 主题 | 文件 |
|------|------|------|
| 🌿 | Vue（默认） | `lib/vue.css` |
| 🌙 | Dark | `lib/dark.css` |
| 💧 | Pure | `lib/pure.css` |
| 🐬 | Dolphin | `lib/dolphin.css` |
| 🫧 | Buble | `lib/buble.css` |

细节：封面页自动隐藏导航栏和滑块；深色主题下刷新时 loading 遮罩也是深色的，不会闪白；遮罩有 4 秒兜底隐藏机制，即使资源加载失败也不会永久白屏。

### 4. 侧边栏（`_sidebar.md`）
文章导航，配置了 `loadSidebar: true` 和 `subMaxLevel: 2`（自动提取二級标题做目录）。

---

## 三、目录结构

```
ThersummerBlog/
├── index.html              ★ 站点入口：docsify 配置、导航栏、主题滑块、遮罩都在这里
├── README.md               首页内容（#/ 路由对应的页面）
├── _sidebar.md             ★ 侧边栏导航（文章目录）
├── _navbar.md              备用原生导航（当前被自定义导航栏隐藏）
├── _coverpage.md           封面页内容
├── zh-cn.md                语言占位文件
├── guide.md                导航栏与主题改造的配置指南
├── lib/                    ★ docsify 4.13.1 本地自托管资源（js + 5 个主题 css）
│   ├── docsify.min.js
│   └── vue.css / dark.css / pure.css / dolphin.css / buble.css
├── images/                 ★ 博客图片资源（按文章分子文件夹）
│   ├── blog.png / avatar.jpg / Lionlogo01.png
│   ├── 个人博客/
│   └── 醒狮社区/
├── 醒狮社区文档/            文章：博客介绍、醒狮社区、更新日志
│   └── 图片/
├── SchoolNetWork/          文章：校园网络笔记（侧边栏入口暂被注释）
├── Ownermd/                文章：个人随笔（侧边栏入口暂被注释）
├── .nojekyll               ★ 告诉 GitHub Pages 不要用 Jekyll 处理（必需）
├── package.json            npm 元数据 + 本地预览脚本
├── 修复报告.md              2026-09 技术修复的详细报告
└── .gitignore
```

★ = 核心文件，改动前建议先备份。

---

## 四、本地启动（预览）

> ⚠️ 注意：docsify 通过 AJAX 拉取 markdown，**直接双击 `index.html` 打不开**（file:// 协议会被浏览器拦截），必须走 HTTP 服务。另外也不要写成 `docsify serve docs`——本项目文件在根目录，没有 `docs` 子文件夹。

**方式一：npm 脚本（推荐，需先安装一次依赖）**

```bash
npm install       # 首次运行，安装 docsify-cli
npm run serve     # 启动预览服务
```

**方式二：docsify 命令**

```bash
docsify serve .   # 注意最后的点，表示当前根目录
# 或
docsify serve
```

**方式三：任意静态服务器**（没装 Node 时）

```bash
python -m http.server 8000
```

启动后浏览器访问：

- `http://localhost:3000`（docsify-cli 默认端口）
- `http://localhost:8000`（python 方式）

---

## 五、如何写新文章

1. **新建 markdown 文件**：放在根目录或按主题建子文件夹（如 `醒狮社区文档/xxx.md`）。
2. **加入侧边栏**：编辑 `_sidebar.md`，按现有格式加一行：

   ```markdown
   * [文章标题](子文件夹/xxx.md)
   ```

3. **插入图片**：统一放在 `images/` 对应子文件夹里，然后引用。**推荐用相对根路径**（不带 `../`）：

   ```markdown
   ![说明](images/子文件夹/图片名.png)
   ```

   > 现有文档中有 `../images/...` 和 `images/...` 两种写法，当前部署方式下都能正常显示，但新文章建议统一用 `images/...`。
4. 保存后刷新浏览器即可看到（docsify 实时渲染，无需重启服务）。

---

## 六、部署到 GitHub Pages

本项目部署流程很简单——推送到 GitHub 即可：

```bash
git add .
git commit -m "feat: 更新文章"
git push origin main
```

GitHub Pages 会自动发布 `main` 分支根目录，稍等一两分钟访问 `https://fogecode.github.io/PersonalBLog.github.io/` 查看效果。

注意两点：

- `.nojekyll` 文件必须保留在根目录（否则 GitHub Pages 用 Jekyll 处理，下划线开头的 `_sidebar.md` 等文件会被忽略，站点会散架）。
- 新增/删除文件记得 `git add` 一并提交，尤其 `lib/` 里的文件是站点运行的必需品。

---

## 七、常见问题（FAQ）

**Q：打开是一直白屏 / LOADING 不消失？**
现在有 4 秒兜底机制，正常不会再出现。若还遇到，按 F12 看控制台报错：检查 `lib/docsify.min.js` 是否能 200 访问（是否正确提交到了 GitHub）。

**Q：本地双击 index.html 打不开 / 样式乱？**
正常现象，见"本地启动"一节，用 `docsify serve .` 或 `python -m http.server` 起服务。

**Q：想改主题列表 / 增删主题？**
改 `index.html` 里主题脚本 IIFE 开头的 `THEMES` 和 `ICONS` 两个数组，把对应 css 放进 `lib/`，滑块会自动适配（`segments` 个数也要同步增删 `index.html` 中 `.seg-item` 元素）。

**Q：封面页怎么改？**
编辑 `_coverpage.md`；封面图片尺寸在 `index.html` 的 `.cover-main img` 样式里调。

**Q：换 Logo 或站名？**
Logo 图片在 `images/blog.png`（导航栏）/ `images/avatar.jpg`（封面），站名文字在 `index.html` 的 `.nav-logo-text` 和 `<title>`。

---

## 八、相关文档

- [醒狮社区文档/Thesummer个人专属博客.md](醒狮社区文档/Thesummer个人专属博客.md) —— 博客搭建过程记录
- [醒狮社区文档/醒狮社区测试.md](醒狮社区文档/醒狮社区测试.md) —— 醒狮社区项目测试记录

---

## 九、修复报告

博客的技术改造与维护记录，也收录在侧边栏"博客说明文档"分支下：

- **[修复报告](修复报告.md)** —— 2026-09 技术修复的完整报告：docsify 本地自托管（消除 BootCDN 供应链风险）、loading 遮罩 4 秒兜底防白屏、深色主题刷新防闪白、主题脚本重构、`.theme-link` 绑定、`package.json` 修正等，含前后代码对比、时序图解与验收截图（`report-assets/`）。
- **[博客改造指南](guide.md)** —— 导航栏与主题切换的配置改造指南：自定义毛玻璃导航栏、五主题滑块、封面页导航控制的实现说明。

> 如果日后对站点做了新的技术改动，建议按"修复报告"的格式追加记录，保持文档与代码同步。
