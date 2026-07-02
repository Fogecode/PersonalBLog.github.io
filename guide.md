# 自定义导航栏与主题切换配置指南

> 本文档记录了本站对 Docsify 默认导航栏的扩展改造，包括：自定义导航菜单、毛玻璃主题切换滑块、封面页导航控制。

---

## 概述

本站对 Docsify 默认的导航系统进行了以下扩展：

- **自定义顶部导航栏**：包含 Logo、文字标识、导航菜单，固定在页面顶部
- **毛玻璃主题切换滑块**：可视化的主题选择器，支持 5 种主题快速切换
- **封面页导航控制**：在封面页自动隐藏顶部导航栏，保持封面纯净

这些改造全部通过 `index.html` 实现，不依赖额外的插件。

---

## 文件结构

```
index.html          ← 所有自定义导航逻辑都在此文件
_navbar.md          ← Docsify 默认导航源文件（需同步维护）
```

---

## 自定义导航栏

### 位置

定义在 `index.html` 的 `<body>` 中：

```html
<div class="custom-navbar">
  <div class="nav-logo">
    <img src="images/blog.png" alt="Logo" class="nav-logo-img">
    <span class="nav-logo-text">ThesummerBlog</span>
  </div>
  <div class="custom-nav-menu">
    <!-- 导航链接 -->
  </div>
</div>
```

### 添加/修改导航项

找到 `index.html` 中 `.custom-nav-menu` 部分：

**普通链接：**
```html
<a class="nav-item" href="#/">🏠 首页</a>
```

**下拉菜单：**
```html
<div class="nav-dropdown">
  <span class="nav-item drop-trigger">分类名 ▾</span>
  <div class="drop-menu">
    <a href="#/path/to/page">页面 A</a>
    <a href="#/path/to/page2">页面 B</a>
  </div>
</div>
```

> ⚠️ **注意**：每次修改此处的导航项时，请同步更新 `_navbar.md`，两者应保持一致。

### 图标支持

导航项可使用任意 Emoji 作为图标，例如：`🏠`、`📖`、`📝`、`🎨`、`🔧`。

---

## 毛玻璃主题切换滑块

### 位置

位于 `index.html` 的 `<body>` 中，独立于导航栏：

```html
<div class="theme-glass-toggle" id="themeGlassToggle">
  <div class="toggle-track">
    <div class="toggle-thumb" id="toggleThumb">
      <span class="thumb-icon" id="thumbIcon">🌿</span>
    </div>
    <div class="toggle-segments" id="toggleSegments">
      <span class="seg-item" data-theme="vue">🌿</span>
      <span class="seg-item" data-theme="dark">🌙</span>
      <span class="seg-item" data-theme="pure">💧</span>
      <span class="seg-item" data-theme="dolphin">🐬</span>
      <span class="seg-item" data-theme="buble">🫧</span>
    </div>
  </div>
</div>
```

### 支持的 5 种主题

| 索引 | 主题名 | 图标 | CSS 文件 |
|------|--------|------|----------|
| 0 | `vue` | 🌿 | `vue.css` |
| 1 | `dark` | 🌙 | `dark.css` |
| 2 | `pure` | 💧 | `pure.css` |
| 3 | `dolphin` | 🐬 | `dolphin.css` |
| 4 | `buble` | 🫧 | `buble.css` |

### 切换原理

1. 点击图标 → JavaScript 切换 `<link id="theme-style">` 的 `href`
2. 选择的主题保存在 `localStorage`（键名：`docsify-theme`）
3. 页面刷新后自动恢复上次选择的主题
4. 滑块位置基于实际 Segment 坐标计算，确保精准对齐

### 自定义主题列表

如需增删主题，需同步修改三处：

**① HTML 中的图标：**
```html
<span class="seg-item" data-theme="vue">🌿</span>
```

**② JavaScript 中的 themes 数组（`index.html`）：**
```javascript
var themes = ['vue', 'dark', 'pure', 'dolphin', 'buble'];
var icons  = ['🌿', '🌙', '💧', '🐬', '🫧'];
```

**③ CSS 中的 body class 清理列表：**
```javascript
document.body.classList.remove('theme-vue', 'theme-dark', 'theme-pure', 'theme-dolphin', 'theme-buble');
```

---

## 封面页导航控制

### 行为

- **封面页（`#/`）**：自动隐藏整个顶部导航栏（Logo、菜单、主题滑块）
- **子页面**：自动显示顶部导航栏

### 实现逻辑

```javascript
function toggleTopBar() {
  var isCover = !location.hash || location.hash === '#/';
  var bar = document.querySelector('.custom-navbar');
  var slider = document.querySelector('.theme-glass-toggle');
  var display = isCover ? 'none' : '';
  if (bar) bar.style.display = display;
  if (slider) slider.style.display = display;
}
window.addEventListener('hashchange', toggleTopBar);
toggleTopBar();
```

> 如需修改封面页显示行为，只需调整此函数即可。

---

## 封面页配置

封面通过 `_coverpage.md` 控制，与导航栏互不干扰：

```markdown
<!-- _coverpage.md -->

![logo](images/avatar.jpg)

# Thesummer个人博客

> 致力自我研究~

- 探索、钻研
- 抛弃传统的word
- 个性化

[GitHub](https://github.com/docsifyjs/docsify/)
[Get Started](Ownermd/a.md)
```

---

## 常见问题

### Q: 添加新页面后导航栏没更新？

需要同时修改两处：
1. `_navbar.md` — Docsify 官方导航
2. `index.html` 中 `.custom-nav-menu` — 实际显示的导航

### Q: 如何调整导航栏高度？

修改 CSS 中 `.custom-navbar` 的 `height` 属性：

```css
.custom-navbar {
  height: 50px;  /* 改为你需要的值 */
}
```

### Q: 主题滑块位置不准怎么办？

检查 `.toggle-track` 的宽度和 `.toggle-segments` 的 padding 是否匹配。位置计算逻辑在 `setTheme()` 函数中：

```javascript
var firstSeg = segments[0];
var lastSeg = segments[segments.length - 1];
var trackRect = track.getBoundingClientRect();
var firstRect = firstSeg.getBoundingClientRect();
var lastRect = lastSeg.getBoundingClientRect();
var firstCenter = (firstRect.left + firstRect.right) / 2 - trackRect.left;
var lastCenter = (lastRect.left + lastRect.right) / 2 - trackRect.left;
var step = (lastCenter - firstCenter) / (segments.length - 1);
thumb.style.left = (firstCenter - 15 + step * index) + 'px';
```

### Q: 如何修改 Logo 图片？

找到 `index.html` 中：

```html
<img src="images/blog.png" alt="Logo" class="nav-logo-img">
```

将 `src` 替换为你的图片路径即可。

---

## 样式参考

导航栏相关 CSS 均位于 `index.html` 的 `<style>` 标签中：

| 选择器 | 作用 |
|--------|------|
| `.custom-navbar` | 顶部导航栏容器 |
| `.nav-logo` | Logo 区域 |
| `.nav-logo-text` | Logo 文字（渐变色） |
| `.custom-nav-menu` | 导航菜单容器 |
| `.nav-item` | 导航链接项 |
| `.nav-dropdown` | 下拉菜单容器 |
| `.drop-menu` | 下拉菜单（毛玻璃效果） |
| `.theme-glass-toggle` | 主题切换滑块容器 |
| `.toggle-track` | 滑块轨道 |
| `.toggle-thumb` | 滑块按钮 |
| `.seg-item` | 主题图标项 |

---

> 本文档随站点导航系统更新。如有功能变更，请同步更新此指南。
