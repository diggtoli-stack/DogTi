# DogTI — Project Context for Claude

## 项目概述

**产品名：** DogTI
**核心概念：** 10题人格测试，MBTI恶搞版，结果是各种"有点不太正常的狗"。
**目标感觉：** 搞笑、有梗、离谱但说中了、互联网感强，像会在朋友圈刷屏的小测试。

---

## 设计原则（不要改动）

- **视觉风格：** 宠物像素风（pixel art pets），参考宠物图鉴截图
- **配色：** 黑字白底，极简 UI
- **禁止：** 深色主题、复杂配色、严肃的 MBTI 风格
- **字体：** 标题用 `Press Start 2P`（Google Fonts），正文用系统字体
- **按钮：** 黑色胶囊形（`border-radius: 100px`），白字，带播放圆圈图标

---

## 文件结构

```
/Users/junli/Desktop/dogti-designs/
├── dogti-main.html        ← 主文件，唯一生产文件
├── style-A-retro-game.html   ← 早期探索稿（暗色GBA主题，存档）
├── style-B-cute-pixel.html   ← 早期探索稿（暖色像素卡片，存档）
└── style-C-meme-chat.html    ← 早期探索稿（聊天气泡梗图风，存档）
```

主文件是**单文件 HTML**，所有 CSS 和 JS 内联，无构建工具，无外部依赖（除 Google Fonts）。

---

## 页面结构（dogti-main.html）

三个页面，通过 `.page` / `.page.active` 切换显示：

| 页面 | ID | 内容 |
|------|-----|------|
| 封面页 | `#page-home` | 像素大标题 DOGTI + 三行滚动像素动物 + 文案 + 开始按钮 |
| 题目页 | `#page-quiz` | 进度条 + 像素狗提示气泡 + 问题文本 + 4个选项(A/B/C/D) |
| 结果页 | `#page-result` | 狗格名称 + 副标题 + 金句 + 性格标签 + 描述 + 分享/再测按钮 |

### 首页关键实现
- 动物滚动带：CSS `@keyframes`，第1、3行向左，第2行向右
- 像素动物：内联 SVG，`image-rendering: pixelated`

---

## 测试逻辑

- **10道题**，每个选项标记 MBTI 维度（E/I、S/N、T/F、J/P）
- `calcResult()` 统计各维度计数，用4个布尔值分支得出结果

### 6种结果（全部为"XX的柴犬"格式）

| 结果名 | 副标题 | SVG key |
|--------|--------|---------|
| 假装冷静的柴犬 | 独居哲学家 | `philosopher` |
| 社恐但好奇的柴犬 | 远程观察员 | `curious` |
| 混乱中立的柴犬 | 随机事件体 | `chaotic` |
| 假装躺平的柴犬 | 看起来很稳实则内卷 | `anxious` |
| 过分理性的柴犬 | 逻辑处理器 | `logical` |
| 社交满能量的柴犬 | 充电宝本人 | `social` |

---

## 结果页文案规范

- 标签文字：**「你的狗格是」**（不是"你的狗型是"）
- 结果格式：`XX的柴犬`

---

## 部署

- **平台：** Cloudflare Pages（主用）→ dogti.pages.dev
- **流程：** 用户确认OK → 推送 GitHub → Cloudflare 自动重新部署
- Vercel（dog-ti.vercel.app）也连着同一仓库，但不再主用

---

## 用户偏好（重要）

- **只改文案时，不动设计和结构**
- 修改某一项时，只改被指定的那一项，其余保持原样
- 不要主动"顺手"优化代码、重构结构、添加功能
