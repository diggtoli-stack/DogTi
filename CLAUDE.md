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
- 像素动物：`<img src="assets/犬种.png">` PNG 文件，`image-rendering: pixelated`
- 标题：`assets/DOGTI标题.png`，文案：`assets/文案.png`

---

## 测试逻辑

- **12道题**，每个选项标记 MBTI 维度（E/I、S/N、T/F、J/P）
- 每题3个选项（A/B/C），选项覆盖不同维度
- `calcResult()` 统计各维度计数，4个维度各取多数，组合成16种 MBTI 类型
- 详细题目、维度映射、结果数据见 → `QUIZ-LOGIC.md`

### 16种结果（格式：XX的犬种）

| MBTI | 结果名 | 犬种 |
|------|--------|------|
| ENTJ | 气场先到三步的杜宾 | doberman |
| ENTP | 把所有人都绕晕了的边牧 | bordercollie |
| ENFJ | 比你更担心你的金毛 | goldenretriever |
| ENFP | 什么都想闻一口的比格 | beagle |
| ESTJ | 把所有人都管住了的德牧 | germanshepherd |
| ESTP | 说好散步结果跑丢的哈士奇 | husky |
| ESFJ | 拒绝不了任何人的拉布拉多 | labrador |
| ESFP | 出门必须好看的泰迪 | poodle |
| INTJ | 假装冷静的柴犬 | shiba |
| INTP | 想到一半就忘了的阿拉斯加 | alaskan |
| INFJ | 永远在笑但只有自己知道为什么的萨摩耶 | samoyed |
| INFP | 你不懂的马尔济斯 | maltese |
| ISTJ | 没做完不能睡觉的柯基 | corgi |
| ISTP | 不需要你担心的松狮 | chow |
| ISFJ | 记住你不喜欢香菜的比熊 | bichon |
| ISFP | 急不起来的腊肠 | dachshund |

---

## 结果页文案规范

- 标签文字：**「你的狗格是」**
- 结果格式：`XX的犬种`（不限柴犬，共16种犬）

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
