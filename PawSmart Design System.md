# PawSmart Design System

> **Product:** PawSmart — "AI Understands Your Dog"
> **Platform:** iOS (iPhone 15 — 393 × 852pt)
> **Version:** 1.0 MVP
> **Last updated:** 2026-03-28

---

## 1. Design Principles

| Principle | Description |
|-----------|-------------|
| **Warm & Friendly** | Approachable and encouraging — not childish, not clinical. Pet owners should feel emotionally connected. |
| **Trust & Professional** | AI-powered, science-backed training. Clean UI communicates reliability and expertise. |
| **Scannable & Action-oriented** | Clear visual hierarchy. One primary action per screen. Users should know what to do within 2 seconds. |
| **Consistent & Systematic** | Every screen follows the same spacing, typography, and component rules. No one-off styles. |

---

## 2. Color System

### Brand Colors

| Token | Hex | Usage |
|-------|-----|-------|
| `primary` | `#FF7A3D` | Brand orange — CTAs, active states, key accents |
| `primary-light` | `#FFF3ED` | Orange tint — highlighted backgrounds, selected states |
| `primary-dark` | `#E5601A` | Pressed/hover state for primary buttons |
| `accent` | `#2D3B8A` | Dark blue — headers, trust elements, emphasis |
| `accent-light` | `#EEF0FF` | Blue tint — informational backgrounds |

### Semantic Colors

| Token | Hex | Usage |
|-------|-----|-------|
| `success` | `#22C55E` | Completed tasks, positive feedback |
| `success-light` | `#F0FDF4` | Success badge/tag background |
| `warning` | `#FCD34D` | In-progress, attention needed |
| `warning-light` | `#FFFBEB` | Warning badge/tag background |
| `error` | `#EF4444` | Error states, destructive actions |

### Neutral Colors

| Token | Hex | Usage |
|-------|-----|-------|
| `bg` | `#FFFFFF` | Page background |
| `surface` | `#F6F7F8` | Card/section surface |
| `text-primary` | `#1A1A1A` | Main body text, titles |
| `text-secondary` | `#6B7280` | Descriptions, secondary info |
| `text-tertiary` | `#6B7280` | Placeholders, meta, disabled text (updated from #9CA3AF for WCAG AA contrast) |
| `border` | `#E5E7EB` | Default borders, dividers |
| `border-subtle` | `#F3F4F6` | Subtle dividers, separator lines |

### Dark Mode Colors

iOS 13+ Dark Mode 适配。开发时通过 `UIColor` / SwiftUI `Color` 的 light/dark trait 实现自动切换。

| Token | Light | Dark | Dark 说明 |
|-------|-------|------|----------|
| `primary` | `#FF7A3D` | `#FF8F5A` | 暗底上略提亮，保持视觉权重 |
| `primary-light` | `#FFF3ED` | `#3D2215` | 橙色调暗底色替代亮底色 |
| `primary-dark` | `#E5601A` | `#CC5517` | 按压态 |
| `accent` | `#2D3B8A` | `#8B9AE8` | 暗底上反转为亮蓝，保持对比度 |
| `accent-light` | `#EEF0FF` | `#1E2244` | 蓝色调暗底色 |
| `success` | `#22C55E` | `#34D16E` | 略提亮 |
| `success-light` | `#F0FDF4` | `#0F2918` | 绿色调暗底色 |
| `warning` | `#FCD34D` | `#FACC15` | 略加饱和 |
| `warning-light` | `#FFFBEB` | `#2D2406` | 黄色调暗底色 |
| `error` | `#EF4444` | `#F87171` | 略提亮保持警示感 |
| `bg` | `#FFFFFF` | `#121212` | Material Design 推荐暗底色 |
| `surface` | `#F6F7F8` | `#1E1E1E` | 卡片/区块表面色 |
| `text-primary` | `#1A1A1A` | `#F5F5F5` | 主文字反转 |
| `text-secondary` | `#6B7280` | `#9CA3AF` | 二级文字提亮一档 |
| `text-tertiary` | `#6B7280` | `#6B7280` | 保持不变（WCAG AA on #1E1E1E = 4.6:1 ✓） |
| `border` | `#E5E7EB` | `#2E2E2E` | 暗底上微弱分隔线 |
| `border-subtle` | `#F3F4F6` | `#252525` | 更微弱的分隔 |

**Dark Mode 组件规则：**
- TabBar pill 背景：`surface` → 边框改用 `border`
- 主按钮：保持 `primary` 填充，文字保持白色
- 卡片：`bg` 填充 + `border` 边框（暗模式下边框更重要）
- 聊天气泡（用户）：保持 `primary` 填充
- 聊天气泡（AI）：`surface` 填充
- 输入框：`surface` 填充 + `border` 边框

---

## 3. Typography

**Font Family:** DM Sans (all weights)

| Style | Size | Weight | Line Height | Usage |
|-------|------|--------|-------------|-------|
| Display | 32px | 700 (Bold) | 1.2 | Large metrics, hero numbers |
| H1 | 24px | 700 (Bold) | 1.3 | Screen titles |
| H2 | 20px | 700 (Bold) | 1.3 | Section headers |
| H3 | 18px | 600 (SemiBold) | 1.3 | Card titles, subsections |
| Body | 15px | 400 (Regular) | 1.5 | Main content, descriptions |
| Body Bold | 15px | 600 (SemiBold) | 1.5 | Emphasized body text |
| Caption | 13px | 500 (Medium) | 1.4 | Labels, tags, metadata |
| Small | 12px | 500 (Medium) | 1.4 | Badges, timestamps |
| Tiny | 11px | 600 (SemiBold) | 1.3 | Tab labels, micro text |

---

## 4. Spacing & Layout

### Screen Dimensions
- **Frame size:** 393 × 852px (iPhone 15)
- **Status bar height:** 62px
- **Tab bar container:** full width, pill height 62px, container padding [12, 21, 21, 21]
- **Safe content area:** ~728px (852 - 62 status - 62 tab area)

### Spacing Scale
| Token | Value | Usage |
|-------|-------|-------|
| `xs` | 4px | Micro gaps (icon-to-text inline) |
| `sm` | 8px | Tight spacing within components |
| `md` | 12px | Card gap, inner element spacing |
| `lg` | 16px | Component padding, medium gaps |
| `xl` | 20px | Content horizontal padding |
| `2xl` | 24px | Section gap (vertical) |
| `3xl` | 32px | Large section separators |

### Content Wrapper
- **Padding:** [0, 20, 24, 20] (top 0 — status bar handles it; right 20; bottom 24; left 20)
- **Layout:** vertical
- **Gap:** 24px (between major sections)

### Corner Radii
| Usage | Radius |
|-------|--------|
| Cards, panels | 20px |
| Inner elements, buttons | 16px |
| Pills, search bars | 26px |
| Badges, tags | 12px |
| Circles (avatars, dots) | 999px |

---

## 5. Component Specifications

### 5.1 Status Bar
- **Size:** 393 × 62px
- **Background:** white (#FFFFFF) or transparent
- **Content:** Time (left), indicators (right) — SF Pro font, 15px, semibold
- **Layout:** horizontal, space_between, alignItems center, padding [0, 20, 0, 20]

### 5.2 Tab Bar (Pill Style)
- **Container:** full width, padding [12, 21, 21, 21]
- **Pill:** fill width, 62px height, corner radius 36px, border 1px #E5E7EB, padding [4, 4]
- **Tab items:** fill_container width & height, corner radius 26px, vertical layout, gap 4px, center aligned
- **Active state:** fill #FF7A3D, icon + label white
- **Inactive state:** transparent, icon + label #9CA3AF
- **Icons:** 18px lucide icons
- **Labels:** 10px, weight 600, uppercase, letter-spacing 0.5px
- **Tabs:** HOME / COURSES / AI / PROFILE

### 5.3 Primary Button
- **Size:** fill width, 56px height
- **Background:** #FF7A3D (primary)
- **Text:** white, 16px, weight 600, center aligned
- **Corner radius:** 16px
- **Pressed state:** #E5601A (primary-dark)

### 5.4 Secondary Button
- **Size:** fill width, 56px height
- **Background:** transparent
- **Border:** 1.5px #FF7A3D
- **Text:** #FF7A3D, 16px, weight 600, center aligned
- **Corner radius:** 16px

### 5.5 Text Button / Ghost Button
- **Size:** fit content
- **Background:** none
- **Text:** #6B7280 (text-secondary), 14px, weight 500
- **Usage:** "Skip", "Continue Free", secondary actions

### 5.6 Input Field
- **Container:** vertical layout, gap 8px
- **Label:** 13px, weight 500, #6B7280
- **Input box:** fill width, 48px height, corner radius 12px, border 1px #E5E7EB, padding [0, 16]
- **Placeholder text:** 15px, weight 400, #9CA3AF
- **Focus state:** border #FF7A3D

### 5.7 Task Card
- **Size:** fill width, auto height
- **Background:** #FFFFFF
- **Border:** 1px #E5E7EB
- **Corner radius:** 20px
- **Padding:** 16px
- **Layout:** horizontal, gap 12px, alignItems center
- **Content:** Checkbox (24px) + vertical (title 15px/600 + duration 13px/400 #6B7280) + progress indicator

### 5.8 Course Card (Vertical)
- **Size:** 170px width (for 2-column grid), auto height
- **Thumbnail:** fill width, 120px height, corner radius 12px (top)
- **Content padding:** 12px
- **Title:** 14px, weight 600, #1A1A1A, max 2 lines
- **Meta:** 12px, weight 400, #6B7280

### 5.9 Chat Bubble — User
- **Alignment:** right
- **Background:** #FF7A3D
- **Text:** white, 15px, weight 400
- **Corner radius:** 20px (top-left, top-right, bottom-left), 4px (bottom-right)
- **Padding:** [12, 16]
- **Max width:** 280px

### 5.10 Chat Bubble — AI
- **Alignment:** left
- **Background:** #F6F7F8
- **Text:** #1A1A1A, 15px, weight 400
- **Corner radius:** 4px (top-left), 20px (top-right, bottom-right, bottom-left)
- **Padding:** [12, 16]
- **Max width:** 280px
- **Avatar:** 32px circle, accent color, paw icon

### 5.11 Badge / Pill Tag
- **Size:** fit content
- **Padding:** [4, 12]
- **Corner radius:** 12px
- **Font:** 12px, weight 500
- **Variants:**
  - Success: bg #F0FDF4, text #22C55E
  - Warning: bg #FFFBEB, text #92700C
  - Primary: bg #FFF3ED, text #FF7A3D
  - Neutral: bg #F6F7F8, text #6B7280

### 5.12 Page Dots (Onboarding)
- **Layout:** horizontal, gap 8px, center aligned
- **Active dot:** 24px × 8px, corner radius 4px, fill #FF7A3D
- **Inactive dot:** 8px × 8px, corner radius 999px, fill #E5E7EB

### 5.13 Feature Card (AI Hub)
- **Size:** fill width, auto height
- **Background:** #FFFFFF
- **Border:** 1px #E5E7EB
- **Corner radius:** 20px
- **Padding:** 20px
- **Layout:** horizontal, gap 16px
- **Icon area:** 48px × 48px, corner radius 12px, tinted background
- **Title:** 16px, weight 600, #1A1A1A
- **Description:** 13px, weight 400, #6B7280

---

## 6. Iconography

- **Icon library:** Lucide
- **Sizes:**
  - Navigation: 24px
  - Actions: 20px
  - Inline: 16px
  - Tab bar: 18px
- **Tab bar icons:**
  - Home: `home`
  - Courses: `book-open`
  - AI: `sparkles`
  - Profile: `user`
- **Common icons:**
  - Camera: `camera`
  - Settings: `settings`
  - Chevron: `chevron-right`
  - Check: `check`
  - Clock: `clock`
  - Trophy: `trophy`
  - Star: `star`
  - Send: `send`

---

## 7. Screen Templates

### Standard App Screen
```
[Status Bar — 62px]
[Content Wrapper — vertical, padding [0, 20, 24, 20], gap 24px]
  [Header / Title area]
  [Primary content]
  [Secondary content]
[Tab Bar — pill style, 4 tabs]
```

### Onboarding Screen (No Tab Bar)
```
[Status Bar — 62px]
[Full Content — vertical, fill]
  [Illustration / visual area — ~50% of screen]
  [Text content — title + subtitle]
  [Page dots]
  [Bottom CTA area — button + skip link]
```

### Modal / Sheet
```
[Overlay — semi-transparent black]
[Sheet — white, rounded top 20px]
  [Handle bar — centered, 40 × 4px, #E5E7EB]
  [Content]
```

---

## 8. Screen Inventory (18 Screens)

| # | Screen | Category | Has Tab Bar |
|---|--------|----------|-------------|
| 1 | Welcome Page 1 | Onboarding | No |
| 2 | Welcome Page 2 | Onboarding | No |
| 3 | Welcome Page 3 | Onboarding | No |
| 4 | Breed Photo Scan | Setup | No |
| 5 | Breed Scan Result | Setup | No |
| 6 | Pet Info Form | Setup | No |
| 7 | Training Questionnaire | Setup | No |
| 8 | Paywall | Conversion | No |
| 9 | Home | Main | Yes (Home) |
| 10 | Course List | Main | Yes (Courses) |
| 11 | Course Detail | Detail | Yes (Courses) |
| 12 | Training In Progress | Detail | No |
| 13 | AI Hub | Main | Yes (AI) |
| 14 | AI Chat | Detail | Yes (AI) |
| 15 | AI Training Plan | Detail | Yes (AI) |
| 16 | Pet Profile | Main | Yes (Profile) |
| 17 | Settings | Detail | Yes (Profile) |
| 18 | Subscription Management | Detail | No |

---

## 9. Design File Organization

### Pencil Canvas Layout
```
Components area (x: -600, y: 0): All reusable components
Row 1 (y: 0):     Screens 1-7 — Onboarding + Pet Setup
Row 2 (y: 920):   Screens 8-12 — Paywall + Main Tabs
Row 3 (y: 1840):  Screens 13-18 — AI + Profile
```
- Screen size: 393 × 852px
- Horizontal gap between screens: 60px

---

## 10. Accessibility (VoiceOver)

### 通用规则
- 所有可交互元素必须有 `accessibilityLabel`
- 装饰性图标/图片设 `accessibilityElementsHidden = true`
- 自定义控件需设置 `accessibilityTraits`（button, header, adjustable 等）
- 最小触控区域 44×44pt（iOS HIG）
- 焦点顺序遵循视觉阅读顺序（从上到下、从左到右）

### 逐屏标注规范

| 屏幕 | 元素 | accessibilityLabel | accessibilityHint | Traits |
|------|------|-------------------|-------------------|--------|
| **Tab Bar** | 首页 Tab | "首页" / "Home" | "显示今日训练任务" | tab, selected |
| | 课程 Tab | "课程" / "Courses" | "浏览训练课程" | tab |
| | AI Tab | "AI 助手" / "AI Assistant" | "智能训练助手" | tab |
| | 档案 Tab | "宠物档案" / "Pet Profile" | "管理宠物信息" | tab |
| **首页** | 连续天数 | "{N} 天连续训练" | — | staticText |
| | 任务卡片 | "{任务名}，{时长}" | "双击开始训练" | button |
| | 完成勾选 | "标记完成" / "已完成" | "双击切换" | button |
| **课程库** | 课程卡片 | "{课程名}，{难度}，{时长}" | "双击查看详情" | button |
| | 锁定课程 | "{课程名}，需要订阅" | "双击查看订阅选项" | button |
| **AI 中心** | 品种识别入口 | "拍照识别狗品种" | "打开相机或相册" | button |
| | AI 助手入口 | "AI 训练助手" | "获取个性化训练建议" | button |
| | 训练计划入口 | "AI 训练计划" | "生成个性化训练计划" | button |
| **AI 聊天** | 消息气泡 | "{发送者}说：{消息内容}" | — | staticText |
| | 输入框 | "输入消息" | "向 AI 助手提问" | searchField |
| | 发送按钮 | "发送" | "发送消息" | button |
| **品种识别** | 拍照按钮 | "拍照识别" | "拍摄狗的照片进行品种识别" | button |
| | 相册按钮 | "从相册选择" | "选择已有照片" | button |
| | 识别结果 | "{品种名}，置信度 {N}%" | — | staticText, header |
| **付费墙** | 方案卡片 | "{方案名}，{价格}，{周期}" | "双击选择此方案" | button |
| | 开始试用 | "开始 7 天免费试用" | "试用结束后按所选方案收费" | button |
| | 跳过 | "跳过，继续使用免费版" | — | button |
| **宠物档案** | 头像 | "{狗名}的照片" | "双击更换照片" | image, button |
| | 信息行 | "{字段}: {值}" | — | staticText |
| | 编辑按钮 | "编辑宠物信息" | — | button |

### VoiceOver 分组规则
- 任务卡片：勾选框 + 标题 + 时长 合并为一个可访问元素
- 课程卡片：缩略图 + 标题 + 时长 合并为一个可访问元素
- 聊天气泡：头像 + 消息文本 合并为一个可访问元素
- 付费方案卡片：价格 + 周期 + 描述 合并为一个可访问元素

### 动态内容通知
- 品种识别完成 → `UIAccessibility.post(.announcement, "识别完成，{品种名}")`
- AI 回复完成 → `UIAccessibility.post(.announcement, "AI 助手已回复")`
- 任务完成打卡 → `UIAccessibility.post(.announcement, "恭喜，任务已完成")`
- 订阅状态变更 → `UIAccessibility.post(.announcement, "订阅状态已更新")`
