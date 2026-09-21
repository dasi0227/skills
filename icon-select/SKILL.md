---
name: icon-select
description: 为界面中的一个或多个对象提供 icon 候选方案，并用极简 HTML 直观展示；当用户要求选择、比较或推荐 icon 方案时使用。
---

# Icon 方案展示

当用户要求给出 icon 方案选择时，只输出一个可直接打开的、自包含的极简 HTML 文件，**禁止附加任何原因解释、长篇分析或复杂交互**。

- 页面使用**浅色纯色背景、居中内容区和灰蓝色文字**；保持充足**留白、细线条和低装饰感**；需要适配窄屏。
- 候选项以**简洁网格**排列，每项只包含等尺寸的 icon 与其名称；优先内联 SVG，避免依赖构建工具。
- 设计多个对象时，需要为每个对象使用**小节标题**分别展示候选网格，相邻小节之间用**粗分隔线**隔开。
- 除非用户另有要求，不加入任何卡片边框、阴影、渐变、说明段落、推荐排序、选中状态或其他装饰性元素。

```html
<!doctype html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>图标候选方案</title>
  <style>
    * { box-sizing: border-box; }
    body {
      margin: 0;
      min-height: 100vh;
      background: #f7f9fc;
      color: #5e6a7d;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
    }
    main { max-width: 760px; margin: 64px auto; padding: 0 32px; }
    h1 { margin: 0 0 48px; color: #273244; font-size: 28px; font-weight: 600; }
    h2 { margin: 0 0 16px; color: #3d495b; font-size: 16px; font-weight: 600; }
    section + section { margin-top: 40px; padding-top: 40px; border-top: 4px solid #dfe5ee; }
    ul {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 8px 24px;
      margin: 0;
      padding: 0;
      list-style: none;
    }
    li { display: flex; min-height: 64px; align-items: center; gap: 14px; font-size: 14px; }
    svg { width: 22px; height: 22px; flex: none; }
    @media (max-width: 580px) {
      main { margin: 32px auto; padding: 0 24px; }
      h1 { margin-bottom: 36px; font-size: 24px; }
      ul { grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 8px 16px; }
    }
  </style>
</head>
<body>
  <main>
    <h1>图标候选方案</h1>

    <section aria-labelledby="repository-title">
      <h2 id="repository-title">仓库</h2>
      <ul>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.75" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><rect width="20" height="5" x="2" y="3" rx="1"/><path d="M4 8v11a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8"/><path d="M10 12h4"/></svg><span>Archive</span></li>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.75" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M21 8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16Z"/><path d="m3.3 7 8.7 5 8.7-5"/><path d="M12 22V12"/></svg><span>Box</span></li>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.75" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M11 21.73a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16V8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73z"/><path d="M12 22V12"/><path d="m3.29 7 8.71 5 8.71-5"/></svg><span>Package</span></li>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.75" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M20 20a2 2 0 0 0 2-2V8a2 2 0 0 0-2-2h-7.9a2 2 0 0 1-1.69-.9L9.6 3.9A2 2 0 0 0 7.93 3H4a2 2 0 0 0-2 2v13a2 2 0 0 0 2 2Z"/></svg><span>Folder</span></li>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.75" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="m16 6 4 14"/><path d="M12 6v14"/><path d="M8 8v12"/><path d="M4 4v16"/></svg><span>Library</span></li>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.75" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="m12.83 2.18 8.59 3.91a1 1 0 0 1 0 1.83l-8.58 3.9a2 2 0 0 1-1.66 0L2.6 7.91a1 1 0 0 1 0-1.83l8.57-3.9a2 2 0 0 1 1.66 0Z"/><path d="m22 12-9.17 4.82a2 2 0 0 1-1.65 0L2 12"/><path d="m22 17-9.17 4.82a2 2 0 0 1-1.65 0L2 17"/></svg><span>Layers</span></li>
      </ul>
    </section>

    <section aria-labelledby="template-title">
      <h2 id="template-title">模板</h2>
      <ul>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.75" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><rect width="18" height="7" x="3" y="3" rx="1"/><rect width="9" height="7" x="3" y="14" rx="1"/><rect width="5" height="7" x="16" y="14" rx="1"/></svg><span>LayoutTemplate</span></li>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.75" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M14.5 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7.5Z"/><path d="M14 2v6h6"/><path d="M8 13h8"/><path d="M8 17h8"/></svg><span>FileText</span></li>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.75" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><rect width="18" height="18" x="3" y="3" rx="2"/><path d="M3 9h18"/><path d="M9 21V9"/></svg><span>PanelsTopLeft</span></li>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.75" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M2 3h20"/><path d="M21 3v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V3"/><path d="m7 21 5-5 5 5"/></svg><span>Presentation</span></li>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.75" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><rect width="14" height="14" x="8" y="8" rx="2"/><path d="M4 16c-1.1 0-2-.9-2-2V4c0-1.1.9-2 2-2h10c1.1 0 2 .9 2 2"/></svg><span>Copy</span></li>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.75" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="m12 3-1.9 5.1L5 10l5.1 1.9L12 17l1.9-5.1L19 10l-5.1-1.9Z"/><path d="M5 3v4"/><path d="M3 5h4"/><path d="M19 17v4"/><path d="M17 19h4"/></svg><span>Sparkles</span></li>
      </ul>
    </section>
  </main>
</body>
</html>
```
