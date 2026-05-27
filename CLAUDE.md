# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

番茄钟（Pomodoro Timer）Web 应用，纯前端单文件实现，无构建步骤、无依赖。

## Running

直接在浏览器中打开 `index.html` 即可，或使用本地服务器：

```bash
# Python
python3 -m http.server 8000

# Node.js
npx serve .
```

## Architecture

所有代码在 `index.html` 中，结构如下：

- **HTML**: 容器布局、计时器圆环、模式选择器、控制按钮、统计面板
- **CSS**: 毛玻璃（glassmorphism）风格，紫色渐变背景，响应式设计
- **JS**: `PomodoroTimer` 类管理全部逻辑
  - 三种模式：pomodoro（25min）、shortBreak（5min）、longBreak（15min）
  - 圆形进度条通过 SVG `stroke-dashoffset` 动画驱动
  - 完成 4 个番茄后自动进入长休息
  - 音频提醒使用外部 CDN（mixkit.co），无本地资源

## Key Considerations

- 修改计时器时长时，同步更新 `this.modes` 和对应 HTML 按钮文本
- 进度条 SVG 圆的 `r=130`，周长约 816.81（`2π × 130`），硬编码在 `stroke-dasharray` 中
- 统计数据（完成番茄数、专注时间）无持久化，刷新页面即丢失
