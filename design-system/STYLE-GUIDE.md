# OCTO Design System · Style Guide

为另一个应用迁移视觉风格时使用本指南。源平台：[OCTO workbench](https://github.com/rainscyy/OCTO)。

---

## 设计原则

**1. 奶油纸基底，不是死白。**  
所有背景层级都在 `#FAF7F1 → #FDFBF7 → #FFFDF9` 之间游走。**禁用纯白 `#FFFFFF`** 作为大块背景（仅用于消息气泡内的高亮代码或对比卡）。

**2. Cobalt 是稀缺资源。**  
钴蓝 `#104BE1` 只用在三种地方：① 主操作按钮 ② 选中态（active tab、selected chip）③ 关键 brand 元素（章鱼 logo）。  
**绝不用 cobalt 作为大块背景**——一个屏幕上的"被点亮"元素应该 ≤ 3 个，否则视觉锚点散掉。

**3. 三层字体职责清晰。**  
| 字体 | 用途 | 不用于 |
| --- | --- | --- |
| **Inter + PingFang SC** | 正文、按钮、表单、菜单 | 不用于 hero |
| **Fraunces + Noto Serif SC** | hero greeting、大标题、卡片 H3 | 不用于正文 |
| **IBM Plex Mono** | eyebrow、元信息、代码、ID、文件名 | 不用于正文段落 |

**4. 圆角分级。**  
小 chip / pill = `999px`（完全圆）；按钮 = `10px`；输入框 / 卡片 = `10–12px`；容器 = `14px`。**禁用 4px 这种 1990s 的尖角**（除了 sticker 便签）。

**5. 阴影克制。**  
默认 elements 不带阴影。**只有 cobalt 主按钮**会有 cobalt-tinted 阴影（`0 2px 6px rgba(16,75,225,0.28)`）来强调"这里是主行动"。其他需要分层的地方用 1px hairline border `rgba(11,18,32,0.08)` 替代阴影。

**6. mono 大写做 eyebrow。**  
所有 section / category 上方的小标签都用 mono + uppercase + `letter-spacing: 0.3-0.5px`，例如 `§ TASK · #T-0248` 或 `WORKSHOP — 3 AGENTS`。这是从 retro 终端继承的视觉语言，**比纯文字标题更有辨识度**。

---

## 色彩使用规则

### Cobalt `#104BE1` — 强调

✅ 用于：
- 主按钮（实心）
- 选中状态（tab.active、chip.is-on）
- 文字链接 hover
- 章鱼 logo
- 进度条 fill

❌ 不用于：
- 大块背景
- 普通文字（除非是链接 / 强调）
- 装饰性图案

### Warn `#B42318` — 危险

✅ 用于：
- HITL 闸门审批卡 dashed 边框
- 删除 / 登出 / 撤销 按钮（outline 变体）
- 余额不足 / 错误状态文字

❌ 不用于：
- 任何"提醒"级别的提示（用 amber `#C68A14` 替代）

### 5 种 Action 类型颜色编码

每种 ADP 资产 / agent 动作都有固定色：

| 类型 | 色 | 触发场景 |
| --- | --- | --- |
| 🔍 search | `#0E8E5C` 绿 | 网页搜索 |
| 📚 knowledge | `#7A4FBE` 紫 | ADP 知识库检索 |
| 🔧 tool | `#104BE1` 蓝 | 调用技能 / 插件 |
| ✏️ edit | `#C68A14` 橙 | 文件编辑 / 起草 |
| 💻 code | `#0B1220` 黑 | 代码生成 / 运行 |

**不要交叉使用**——读者建立色彩肌肉记忆后，扫一眼就能判断 agent 当前在做什么。

---

## 间距系统

只用 `4 · 8 · 12 · 16 · 22 · 32 · 48 · 64` 这 8 个值（tokens 里的 `--sp-1 → --sp-8`）。**禁止 7px、13px、19px** 这种"差不多"的值——会让对齐崩。

主区域内容宽度上限 = `720px`（`--content-max`），超出后两侧留白。

---

## 组件 dos & don'ts

### Buttons

✅ 一个屏幕只有 ONE 主按钮（`btn-primary`）  
✅ 次按钮成组时用 `btn`（默认）或 `btn-ghost`  
❌ 不要把 ghost 按钮和 primary 按钮放一组——视觉权重崩  
❌ 不要在主按钮里塞 emoji / 装饰 icon

### Chips

✅ 默认状态轻量（mut 灰文字 + paper 底）  
✅ Selected 时填实心 cobalt + 白字  
❌ 不用 chip 做"导航"（用 tab）；chip 是过滤器 / 选项  
❌ 一行 chip 不超过 7 个，超出折行或加溢出菜单

### Inputs

✅ Focus 状态必须有 cobalt 描边 + 浅 cobalt 光晕  
✅ Search 类输入要把图标绝对定位在 left:12px  
❌ 不要用 4 路阴影做"凹陷感" — 用 1px border 就够

### Conversation Lane（OCTO 核心）

按这个顺序渲染每个 agent 回应：

```
┌─ details.thinking         ← 折叠 mono 块（默认收起）
├─ action.is-knowledge      ← 第一张动作卡
├─ action.is-tool           ← 第二张
├─ action.is-edit           ← 第三张
├─ <octopus mark>           ← 章鱼像素 logo
├─ msg-text                 ← 流式打字主文本
├─ code-block               ← 暗色代码块（可选）
└─ src-pill src-pill src-pill  ← 来源 chip
```

**关键交互细节：**
- 思考块进行时 dot 跳动（`@keyframes pulse`）→ 完成时 dot 切绿且停止动画 → summary 文字从"思考 · 进行中"变"思考 · 已用 1.2s"
- Action 卡渲染时 icon pulse → 完成后停止
- 文本流式打字（每字符 `12-16ms` 间隔 + 闪烁 caret `.blinky`）

### HITL Approval Card

✅ 必须包含三件信息：**本步预算 · 影响面 · 回滚方案**  
✅ 四按钮顺序：**Accept · Decline · Pause · Replace**  
❌ 不用 modal 弹窗——用 inline dashed 边框卡（让用户保持在对话上下文里）

---

## 迁移检查清单

把 OCTO 视觉迁到另一个 app 时，按这个顺序检查：

- [ ] 引入 `tokens.css`（全局，最优先）
- [ ] 加载 4 个字体（Inter / PingFang SC / Fraunces / Plex Mono）
- [ ] 全局 `body` 改用 `var(--paper)` 底 + `var(--sans)` 字体
- [ ] 所有按钮替换为 `.btn / .btn-primary / .btn-ghost`
- [ ] 所有 chip / pill / tab 替换为新组件
- [ ] 输入框换成 `.input` 风格（focus cobalt 光晕）
- [ ] 卡片底色改 `--paper-2`，圆角 `--r-lg`
- [ ] **删除原 app 里所有硬编码颜色**（grep `#[0-9a-f]{6}` 找出来）
- [ ] **删除原 app 里所有 `font-family` 直接定义**（统一用 token）
- [ ] **删除多余阴影**（保留 token 里的 `--shadow-1/2/cobalt`）
- [ ] 字体不可用时 fallback 到 system-ui（已在 token 里写好）
- [ ] dark mode 暂不支持 —— 如需暗色，单独再做一个 token 集

---

## 不要做的事

❌ **不要**改 OCTO token 名（如把 `--cobalt` 改成 `--brand-blue`）—— 跨项目复用会迷路  
❌ **不要**新增新色板——所有颜色都应能从现有 token 派生  
❌ **不要**绕过 token 直接写颜色值  
❌ **不要**把 sticker 视觉用在非"任务便签"语义的地方（仅限 task list / memo board）  
❌ **不要**让对话气泡背景比 paper 更深——会破坏阅读节奏  
❌ **不要**用动画过渡颜色——只过渡 `transform / opacity / background / border-color`，时长 `0.12-0.18s`

---

## 参考实现

| 文件 | 用途 |
| --- | --- |
| `tokens.css` | 所有 CSS 变量，**先引入这个** |
| `components.html` | 浏览器打开看实物，复制 markup 到你的应用 |
| OCTO 源码 | https://github.com/rainscyy/OCTO （需要更深 reference 时来这查） |

---

## 字体许可

| 字体 | 许可 | 商用 OK? |
| --- | --- | --- |
| Inter | OFL 1.1 | ✓ |
| Fraunces | OFL 1.1 | ✓ |
| IBM Plex Mono | OFL 1.1 | ✓ |
| Noto Serif SC | OFL 1.1 | ✓ |
| PingFang SC | Apple system font | 仅 macOS / iOS 自带，无需嵌入 |

可放心商用。需自托管时，从 [Google Fonts](https://fonts.google.com) 或 [GitHub IBM Plex](https://github.com/IBM/plex) 下载。

---

## 版本

`v1.0` · 2026-04 · [Raine (沙纯钰)](mailto:chunyu_sha@gsd.harvard.edu)

更新日志维护在 OCTO repo 主分支。
