# Architecture

## 系统架构

这是一个纯前端项目，不涉及后端或数据库。所有资源（HTML、CSS、媒体文件）都是本地的。

## 源码路径

- `index.html`: 项目的唯一页面，包含了所有的 HTML 结构、CSS 样式和 JavaScript 逻辑。
- `视频.mp4`: 背景视频文件。
- `音频.mp3`: 背景音频文件。

## 关键技术决策

- **纯 HTML/CSS/JS**: 为了简单起见，不使用任何前端框架。
- **CSS `object-fit`**: 使用 `object-fit: cover` 属性来确保视频铺满屏幕而无拉伸。
- **HTML5 `<video>` 和 `<audio>` 标签**: 使用标准 HTML5 元素来播放媒体，并利用 `autoplay` 和 `loop` 属性实现自动和循环播放。
- **CSS `transition`**: 用于实现情诗文本的渐隐渐显动画，比复杂的 `@keyframes` 更简洁高效。
- **JavaScript `setInterval`**: 用于创建定时循环，以固定间隔切换情诗。

## 设计模式

该项目非常简单，未使用复杂的设计模式。主要是一种声明式的页面结构，通过 JavaScript 进行状态管理（如当前诗歌索引）。

## 组件关系

- `<body>` 元素包含了 `<video>`、`<audio>` 和 `#poem-container` 三个核心元素。
- `#poem-container` 内部包含 `#poem-text`，用于显示具体的诗歌内容。
- CSS 样式直接应用于 `<body>`、`#bg-video`、`#poem-container` 和 `#poem-text` 等 ID 选择器，并通过 `z-index` 确保 `#poem-container` 位于 `#bg-video` 之上。

## 关键实现路径

1. HTML 文件加载，同时通过 CDN 异步加载外部字体。
2. 浏览器解析 DOM，找到 `<video>`、`<audio>` 和情诗容器等元素。
3. 视频通过 `autoplay` 和 `muted` 属性自动静音播放。
4. JavaScript 脚本尝试自动播放音频。如果失败，则会设置一个一次性的事件监听器，在用户首次与页面交互（例如点击）时播放音频。
5. JavaScript 脚本初始化情诗功能：从内置数组中随机选择一首诗立即显示。
6. 启动一个 `setInterval` 定时器，每10秒执行一次情诗切换函数。
7. 切换函数通过增删 CSS class 来触发 `opacity` 的 `transition` 动画，实现渐隐渐显效果。
8. CSS 确保 `<video>` 元素作为背景全屏显示，并确保情诗容器固定在页面的特定位置。
9. `loop` 属性确保媒体在播放结束后自动重新开始。
