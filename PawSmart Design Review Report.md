# PawSmart Design Review Report

> **Product:** PawSmart — "AI Understands Your Dog"
> **Review Type:** 7-Pass Designer's Eye Review (`/plan-design-review`)
> **Date:** 2026-03-29
> **Reviewer:** Claude (AI Design Reviewer)
> **Artifacts Reviewed:** PawSmart Design System.md, PRD, 18-screen Pencil prototype (pencil-new.pen)
> **Review Runs:** 2 (Run 1: baseline review → Run 2: deep review with outside voices)

---

## Review Summary

| Dimension | Run 1 Initial | Run 1 Final | Run 2 Initial | Run 2 Final | Key Actions |
|-----------|---------------|-------------|---------------|-------------|-------------|
| Overall Design Score | **7/10** | **8/10** | **8/10** (re-baselined 6/10) | **9/10** | 23 decisions made, 0 deferred |
| Pass 1: Information Architecture | 7/10 | 8/10 | 7/10 | 9/10 | +Login screen, offline UX, warning cards, subscription UX, usage indicators |
| Pass 2: Interaction States | 2/10 | 6/10 | 6/10 | 9/10 | Skeleton screens, 6 error scenarios, 5 success states, 6 progress states |
| Pass 3: User Journey | 6/10 | 7/10 | 7/10 | 9/10 | Soft upgrade transition, Day 2-7 return, pet elements in settings |
| Pass 4: AI Slop Risk | 8/10 | 9/10 | 9/10 | 9/10 | AI Hub redesign confirmed built, no new issues |
| Pass 5: Design System Alignment | 8/10 | 8/10 | 8/10 | 9/10 | Font unified to DM Sans, PRD correction |
| Pass 6: Responsive & Accessibility | 3/10 | 6/10 | 6/10 | 8/10 | Defensive Dynamic Type rules |
| Pass 7: Unresolved Decisions | — | 7 resolved | — | +2 resolved | Tab badges, paywall dual strategy |

---

## Step 0: Design Scope Assessment

### Run 1 — Initial Rating: 7/10

**Strengths (earning the 7):**
- Complete design system with 17 color tokens, 9 typography styles, 13 components
- All 18 screens built with consistent component reuse
- Clear visual hierarchy — orange primary CTA always prominent
- Distinctive pill-style tab bar
- Proper iPhone 15 frame (393×852px) with consistent layout

**Gaps (preventing 10):**
1. No interaction states (loading, empty, error, partial)
2. No empty states designed
3. Onboarding illustrations are placeholder
4. No micro-interactions or transitions
5. Accessibility specs missing (contrast, touch targets, screen readers)
6. Edge cases unaddressed (long names, 0 streak, free vs premium)
7. Screen 9 (Home) is visually dense

### Run 2 — Re-baselined to 8/10

All 4 Run 1 action items confirmed built in prototype:
- ✅ 5 empty state screens (9b, 10b, 14b, 15b, 16b)
- ✅ AI Hub redesign (hero card + 2 tiles)
- ✅ Celebration modal (Screen 12b)
- ✅ Contrast fix (text-tertiary updated to #6B7280)

Re-baselined from 6/10 (deeper audit revealed gaps in login, offline, interaction states) with goal of 9/10.

### Outside Design Voices (Run 2)

**Codex + Claude subagent** ran independently. Litmus scorecard:

```
DESIGN OUTSIDE VOICES — LITMUS SCORECARD:
═══════════════════════════════════════════════════════════════
  Check                                    Claude  Codex  Consensus
  ─────────────────────────────────────── ─────── ─────── ─────────
  1. Brand unmistakable in first screen?   YES     YES    CONFIRMED
  2. One strong visual anchor?             YES     YES    CONFIRMED
  3. Scannable by headlines only?          YES     YES    CONFIRMED
  4. Each section has one job?             YES     YES    CONFIRMED
  5. Cards actually necessary?             MOSTLY  YES    CONFIRMED
  6. Motion improves hierarchy?            NOT YET NOT YET CONFIRMED GAP
  7. Premium without decorative shadows?   YES     YES    CONFIRMED
  ─────────────────────────────────────── ─────── ─────── ─────────
  Hard rejections triggered:               0       0      0
═══════════════════════════════════════════════════════════════
```

### DESIGN.md Status
`PawSmart Design System.md` exists and is comprehensive. All decisions calibrated against it.

### Existing Design Leverage
13 reusable Pencil components, 17 color variables, established content wrapper pattern, section header with "See All" pattern, card border pattern, pill tab bar. 24 screens in prototype (18 main + celebration modal + 5 empty states).

---

## Pass 1: Information Architecture — 7/10 → 8/10 → 9/10

### Decision 1: Training Completion Navigation (Run 1)
> **Question:** Where does "Done" on Training In Progress (Screen 12) take the user?
>
> **Options considered:**
> - A) Done → Course Detail ← **SELECTED**
> - B) Done → Home
> - C) Done → Completion Modal then choice
>
> **User chose: A — Done → Course Detail**

**Spec:** Completing training returns to Course Detail, where user sees updated progress and can start next step. Back arrow on Course Detail returns to Course List.

**Rationale:** Keeps user in the course context, encourages completing multiple steps in one session.

---

### Decision 8: Login Screen Addition (Run 2)
> **Question:** PRD 7.5 定义了完整的账号体系（Sign in with Apple 优先），但原型没有登录/注册屏幕。引导流程起点是 Welcome Page，但用户什么时候登录？
>
> **Options considered:**
> - A) 新增登录屏幕到原型 ← **SELECTED**
> - B) 延后到开发阶段
>
> **User chose: A — 新增登录屏幕**

**Spec:**
- 插入位置：Welcome Page 3 之后、Breed Photo Scan 之前
- 布局：品牌 Logo + 宠物插图（上 40%）→ "Sign in with Apple" 按钮（Primary, 56px）→ Email 登录（Secondary）→ "Continue as Guest"（Text Button）→ 底部隐私政策链接
- Guest 模式：可完成引导流程，但打卡/AI 数据仅本地存储，触达付费墙时必须登录

---

### Decision 9: Offline State UX Rules (Run 2)
> **Question:** PRD 7.6 补充了离线策略矩阵，但原型没有任何离线状态的视觉表达。用户在公园训练时断网，看到什么？
>
> **Options considered:**
> - A) 定义离线状态 UX 规则 ← **SELECTED**
> - B) 延后到开发阶段
>
> **User chose: A — 定义离线状态 UX 规则**

**Spec:**
- 全局离线指示器：顶部 Toast 条，#FFFBEB 背景 + ⚡ 图标 + "离线模式 — 部分功能受限"，高度 36px，DM Sans 13px/500
- 功能分级：
  - 🟢 正常可用：已缓存任务卡、已缓存课程文字步骤、宠物档案
  - 🟡 降级可用：打卡（本地排队 + 角标 "待同步"）、课程列表（仅已缓存）
  - 🔴 不可用：AI 聊天（输入框禁用 + "需要网络连接"）、视频播放（显示占位图 + "连接网络后播放"）、品种识别（"需要网络连接"）
- 恢复联网时：自动同步 + Snackbar "已同步 X 条打卡记录"

---

### Decision 10: Warning Card Spec (Run 2)
> **Question:** PRD 定义了多种需要用户注意的系统状态（AI 模型下载中、订阅即将到期、打卡待同步），但原型没有统一的警告/提醒卡片组件。
>
> **Options considered:**
> - A) 定义专门的警告卡片规格 ← **SELECTED**
> - B) 复用现有组件
>
> **User chose: A — 定义专门的警告卡片规格**

**Spec:**
- 容器：fill width, auto height, cornerRadius 16px, padding [12, 16]
- 布局：horizontal, gap 12px, alignItems center
- 图标区：32×32px, cornerRadius 8px
- 三种变体：
  - Info（蓝色）：bg #EEF0FF, icon #2D3B8A, 场景：模型下载进度、新功能提示
  - Warning（黄色）：bg #FFFBEB, icon #92700C, 场景：订阅即将到期、存储空间不足
  - Urgent（橙色）：bg #FFF3ED, icon #FF7A3D, 场景：试用到期倒计时、打卡待同步
- 可选 CTA：右侧 Text Button 或 Chevron

---

### Decision 11: Subscription State Change UX (Run 2)
> **Question:** PRD 7.8 定义了 6 种订阅状态（active/trial/grace_period/expired/cancelled/free），但原型没有展示状态变更时用户看到什么。
>
> **Options considered:**
> - A) 定义订阅状态变更 UX ← **SELECTED**
> - B) 延后到开发阶段
>
> **User chose: A — 定义订阅状态变更 UX**

**Spec:**
- Trial → Active（续费成功）：无打扰，静默过渡
- Trial → Expired（未续费）：Warning 卡片（首页顶部）→ 3天后降级为 free，锁定 Premium 内容
- Active → Grace Period（扣费失败）：Urgent 卡片 "支付失败，请更新付款方式" + CTA → 系统设置
- Active → Cancelled（用户取消）：Info 卡片 "Premium 有效至 [日期]" + 剩余天数
- Any → Free（降级完成）：全屏过渡页 "你的 Premium 已结束" + 保留的数据摘要 + "重新订阅" Primary CTA + "继续免费" Text Button
- 降级后内容处理：Premium 课程显示锁 + "PRO" 徽章，已完成的进度数据保留可见但新课程锁定

---

### Decision 12: Usage Indicators (Run 2)
> **Question:** PRD 定义了免费用量限制（品种识别 3次/天、AI 助手 5条/天），但用户何时、在哪里看到剩余用量？
>
> **Options considered:**
> - A) 确认并细化用量指示器 ← **SELECTED**
> - B) 仅在达限时提示
>
> **User chose: A — 确认并细化用量指示器**

**Spec:**
- AI 聊天：输入框上方 Caption 文字 "3/5 messages today"，颜色随用量变化（≥3 剩余 #6B7280 → 1 剩余 #FF7A3D → 0 剩余 #EF4444 + 输入框禁用）
- 品种识别：扫描按钮下方 "2 scans remaining today"，同色变化规则
- 达限后：输入/按钮替换为 "Upgrade to unlock unlimited" Primary Button
- Premium 用户：不显示用量计数器

---

## Pass 2: Interaction State Coverage — 2/10 → 6/10 → 9/10

### Decision 2: Empty State Specifications (Run 1)
> **Question:** Should we add empty state specs to the plan?
>
> **Options considered:**
> - A) Top 5 empty states ← **SELECTED**
> - B) Top 3 only
> - C) Defer all to implementation
>
> **User chose: A — Define 5 empty states**

**Empty States Specified:**

| Screen | Trigger | Visual | Primary Action |
|--------|---------|--------|----------------|
| Home (first-time) | Day 1 user | Paw illustration + "Let's start your first training!" | "Choose a Course" button |
| Course List (empty) | No enrolled courses | Dog with book illustration + "Your journey starts here" | "Browse Courses" / "Try Free Course" |
| AI Chat (first message) | No conversation yet | AI avatar + greeting + 3 suggested prompt chips | Tap chip or type |
| Training Plan (none) | No plan generated | Calendar illustration + "Get a personalized plan" | "Generate My Plan" button |
| Pet Profile (new) | 0 stats | Pet avatar + all stats showing "0" + encouragement | "Start First Lesson" button |

---

### Decision 13: Skeleton Screen Unified Spec (Run 2)
> **Question:** Run 1 定义了 "Skeleton screens (gray shimmer), never spinners"，但没有具体视觉规格。9 个需要骨架屏的屏幕（首页、课程列表、课程详情、AI 聊天、AI 计划、宠物档案、设置、订阅管理、品种结果）各自什么样？
>
> **Options considered:**
> - A) 定义骨架屏统一规格 ← **SELECTED**
> - B) 仅定义 3 个核心屏幕
>
> **User chose: A — 定义骨架屏统一规格**

**Spec:**
- 基础形状：圆角矩形, fill #F3F4F6, cornerRadius 8px
- 动画：左→右 shimmer 渐变（#F3F4F6 → #E5E7EB → #F3F4F6），周期 1.5s，ease-in-out
- 文字占位：高度与实际字号匹配（标题 24px → 占位条 24px 高），宽度 60-80%
- 图片占位：与实际尺寸匹配，cornerRadius 与实际一致
- 头像占位：圆形，与实际尺寸匹配
- 超时规则：3s 内未加载完成 → 显示骨架屏；10s 超时 → 切换为错误状态
- 覆盖 9 个屏幕：Home, Course List, Course Detail, AI Chat, AI Plan, Pet Profile, Settings, Subscription, Breed Result

---

### Decision 14: Error Scenarios (Run 2)
> **Question:** Run 1 定义了 3 种错误类型（网络/AI超时/相机），但 PRD 修订后新增了更多错误场景。6 种关键错误场景需要完整视觉定义。
>
> **Options considered:**
> - A) 6 种错误场景全部定义 ← **SELECTED**
> - B) 仅定义 3 种核心错误
>
> **User chose: A — 6 种错误场景全部定义**

**Spec:**

| 错误场景 | 触发条件 | 视觉表现 | 恢复操作 |
|---------|---------|---------|---------|
| 视频播放失败 | HLS 加载失败 / 缓冲超时 15s | 视频区域显示 play 图标 + "无法播放视频" + "重试" 按钮 | 重试 / 切换到文字步骤 |
| 训练计划生成失败 | LLM 超时 / 服务不可用 | 生成区域显示 "计划生成失败" + "使用推荐计划" 按钮 | 重试 / 使用模板计划 |
| StoreKit 购买失败 | Apple 系统问题 / 网络中断 | 全屏 Alert "购买未完成" + 错误原因 + "重试" + "稍后再试" | 重试 / 关闭 |
| 登录失败 | Apple ID 服务不可用 / 网络 | 登录按钮下方 inline 错误文字 #EF4444 + "请检查网络后重试" | 重试 / Guest 模式 |
| 数据同步失败 | 离线打卡同步冲突 | Snackbar "部分数据同步失败" + "查看详情" | 查看冲突 / 忽略 |
| AI 模型下载失败 | 网络中断 / 存储不足 | Info 警告卡 "AI 模型下载中断" + 进度条 + "继续下载" | 继续下载 / 使用云端 |

---

### Decision 15: Success States (Run 2)
> **Question:** 产品中有多种成功场景（订阅成功、计划生成完成、档案编辑保存、数据同步完成、登录成功），每种的视觉反馈应该匹配操作的「重量感」。
>
> **Options considered:**
> - A) 定义全部 5 种成功状态 ← **SELECTED**
> - B) 仅定义 3 种核心成功状态
>
> **User chose: A — 定义全部 5 种成功状态**

**Spec:**

| 成功场景 | 视觉反馈 | 时长 | 后续动作 |
|---------|---------|------|---------|
| 订阅成功 | 全屏庆祝页：confetti + "Welcome to Premium!" + 宠物头像 + 解锁功能列表 | 用户主动关闭 | "Start Exploring" → Home |
| 训练计划生成 | Inline 展开动画 + Toast "Your plan is ready!" + 计划卡片入场动画 | Toast 3s | 查看计划详情 |
| 档案编辑保存 | Toast "Saved!" + ✓ 图标，#22C55E | 2s 自动消失 | 停留当前页 |
| 数据同步完成 | Snackbar "Synced X records" + ✓ | 3s 自动消失 | 无 |
| 登录成功 | 过渡页 "Welcome, [name]!" + 宠物插图 | 1.5s 自动跳转 | → 引导流程或 Home |

---

### Decision 16: Progress States (Run 2)
> **Question:** 6 种需要等待的操作（AI 模型下载、训练计划生成、跨天任务刷新、视频缓冲、离线同步、StoreKit 处理）各需要不同的进度反馈。
>
> **Options considered:**
> - A) 定义全部 6 种进度状态 ← **SELECTED**
> - B) 仅定义 3 种核心进度状态
>
> **User chose: A — 定义全部 6 种进度状态**

**Spec:**

| 等待场景 | 视觉反馈 | 预期时长 | 超时处理 |
|---------|---------|---------|---------|
| AI 模型下载 | 圆形进度环 + 百分比 + "Downloading AI Model..." | 30s-3min | 暂停/继续按钮 |
| 训练计划生成 | 3 步动画（分析档案→匹配课程→生成计划）+ 每步 ✓ 完成 | 5-15s | 15s 后 "Taking longer than usual..." |
| 跨天任务刷新 | 顶部进度条（细线，#FF7A3D，从左到右）| 1-3s | 3s 后显示上次缓存 |
| 视频缓冲 | 视频区域中心 spinner + 已加载百分比 | 2-10s | 10s 后建议切换画质 |
| 离线数据同步 | Snackbar "Syncing..." + 旋转图标 | 2-10s | 10s 后 "Sync taking longer..." |
| StoreKit 处理 | 购买按钮变为 loading 状态（spinner 替换文字）| 2-10s | 10s 后 "Still processing..." |

**交互状态覆盖率：** 9/38 (24%) → 38/38 (100%)

---

## Pass 3: User Journey & Emotional Arc — 6/10 → 7/10 → 9/10

### Decision 3: Training Completion Celebration (Run 1)
> **Question:** What celebration pattern for completing a training task?
>
> **Options considered:**
> - A) Completion modal with confetti + stats ← **SELECTED**
> - B) Inline success state (green checkmark, auto-return)
> - C) Defer to implementation (simple toast)
>
> **User chose: A — Completion modal with stats**

**Celebration Modal Spec:**
- **Trigger:** User taps "Done" on Training In Progress
- **Visual:** Overlay modal with paw-print confetti animation
- **Content:**
  - "Great job, [pet name]!" (24px, bold, #1A1A1A)
  - Stats row: time trained | reps completed | step progress
  - First-time bonus: "First Lesson Complete!" badge with star, #FF7A3D
  - Streak update: "+1 Day Streak" if applicable
- **Actions:** "Next Step" (primary) | "Back to Course" (text button)
- **Animation:** 1.5s confetti burst, modal slides up from bottom

---

### Decision 17: Soft Upgrade Transition (Run 2)
> **Question:** 免费试用到期后，用户体验是「悬崖式」（突然锁定一切）还是「柔性过渡」？悬崖式转化率低且伤害用户情感。
>
> **Options considered:**
> - A) 设计「柔性升级」过渡体验 ← **SELECTED**
> - B) 沿用标准硬切方案
>
> **User chose: A — 设计「柔性升级」过渡体验**

**Spec — 3 阶段柔性过渡：**
1. **Phase 1: 预警期（到期前 48h）**
   - 首页顶部 Warning 卡片（黄色）："Your trial ends in 2 days"
   - 轻触可展开查看已解锁的功能列表
   - 不阻断任何功能使用
   - 到期前 24h 卡片升级为 Urgent（橙色）

2. **Phase 2: 价值回顾（到期时刻）**
   - 底部弹出 Sheet（60% 屏幕高度）
   - 展示个人成就：完成 X 节课、连续打卡 Y 天、[pet name] 学会了 Z 个技能
   - "Keep your progress" Primary CTA
   - "Maybe later" Text Button（关闭 sheet，进入 Phase 3）

3. **Phase 3: 降级体验（到期后）**
   - Premium 内容显示毛玻璃 blur + 锁图标
   - 已完成课程的进度数据可见（不可操作新课程）
   - 首页任务仅显示免费课程的任务
   - AI 聊天恢复 5条/天限制，品种识别恢复 3次/天

---

### Decision 18: Day 2-7 Return Experience (Run 2)
> **Question:** 用户第 2-7 天回来时，首页应该和 Day 1 有什么不同？习惯形成的关键 7 天内，每次回来都应该感受到进步和个性化。
>
> **Options considered:**
> - A) 定义 7 天回归体验设计 ← **SELECTED**
> - B) 首页保持静态
>
> **User chose: A — 定义 7 天回归体验设计**

**Spec:**
- **动态问候语：** 根据时间段变化（"Good morning, [pet name]'s human!" / "Evening training time!"），非固定 "Welcome back"
- **Streak Bar：** 首页 header 下方，7 格进度条，已完成天用 #FF7A3D 填充 + ✓，今天用脉冲动画高亮，未来天用 #E5E7EB
- **成长数据：** 每次回来显示新进度（"[pet name] learned 2 new skills this week" / "+3 lessons since last visit"）
- **AI 推荐：** Day 3+ 出现 AI 推荐卡片（"Based on [pet name]'s progress, try: [course name]"），使用 accent-light 背景
- **视觉差异保证：** 每天至少 3 个视觉元素变化（问候语、streak、推荐内容），避免「每天看到一样的页面」

---

### Decision 19: Pet Elements in Settings/Subscription (Run 2)
> **Question:** 设置页和订阅管理页是纯工具页面，完全没有宠物元素。对于一个宠物训练 App 来说，这些页面也应该让用户感受到「这是为我的狗做的」，而不是通用 SaaS 设置页。
>
> **Options considered:**
> - A) 在设置/订阅页添加宠物元素 ← **SELECTED**
> - B) 维持工具页风格
>
> **User chose: A — 在设置/订阅页添加宠物元素**

**Spec:**
- **宠物档案 Tab（Screen 16）→ 设置入口：** 顶部显示宠物头像 + 名字 + 品种 + "Training since [date]"，设置按钮从头像区进入
- **设置页（Screen 17）：** 顶部添加训练成果摘要卡（"[pet name]: X lessons completed, Y day streak"），使用 primary-light 背景
- **订阅管理页（Screen 18）：** 添加 "What [pet name] gets with Premium" 个性化功能列表；取消订阅流程增加情感化文案（"[pet name] will miss the advanced courses..."）

---

## Pass 4: AI Slop Risk — 8/10 → 9/10

**Classification:** APP UI (with onboarding/marketing hybrid screens)

### Hard Rejection Check: 0 rejections triggered
- ✅ No generic SaaS card grid as first impression
- ✅ No weak brand imagery
- ✅ Clear CTAs on every screen
- ✅ Clean backgrounds, no busy imagery
- ✅ No repeated mood statements
- ✅ No purposeless carousels
- ⚠️ Borderline: Home and AI Hub rely on card stacks (Run 1) → **Resolved:** AI Hub redesigned (Run 1 Decision 4)

### Litmus Checks:
| Check | Result |
|-------|--------|
| Brand unmistakable in first screen? | ✅ YES |
| One strong visual anchor? | ✅ YES |
| Scannable by headlines only? | ✅ YES |
| Each section has one job? | ✅ YES |
| Cards actually necessary? | ✅ YES (after AI Hub redesign) |
| Motion improves hierarchy? | ⚠️ PARTIALLY (confetti + shimmer spec'd, more in v1.1) |
| Premium without decorative shadows? | ✅ YES |

### Decision 4: AI Hub Redesign (Run 1)
> **Question:** Screen 13 (AI Hub) has 3 identical feature cards — the #2 most recognizable AI-generated layout pattern.
>
> **Options considered:**
> - A) Redesign with hero card + 2 tiles ← **SELECTED**
> - B) Keep cards, add visual differentiation
> - C) Accept current design
>
> **User chose: A — Redesign AI Hub layout**

**New Layout:**
- **Hero card (AI Chat):** Full-width, 180px, AI avatar illustration, gradient bg (#FF7A3D → #E5601A), white text "Chat with your AI trainer"
- **Two action tiles below:** Side-by-side (2-column), smaller square tiles for "Breed Scan" and "Training Plan". Surface bg with subtle orange accent.
- **Confirmed built in prototype** ✅

---

## Pass 5: Design System Alignment — 8/10 → 9/10

**Well-aligned (both runs):**
- 17 color tokens consistently applied
- 20px content padding, 24px section gaps per spec
- 13 reusable components used via `ref` instances
- Corner radii consistent (20px cards, 16px buttons, 26px pills)
- Pill-style tab bar matches spec exactly

### Decision 20: Font Unification (Run 2)
> **Question:** Design System 和原型全部使用 DM Sans，但 PRD 第 6.1 节写的是 SF Pro。两个文档不一致会导致开发困惑。
>
> **Options considered:**
> - A) 统一为 DM Sans，修正 PRD ← **SELECTED**
> - B) 改为 SF Pro
>
> **User chose: A — 统一为 DM Sans，修正 PRD**

**Action:** PRD 第 6.1 节「SF Pro」改为「DM Sans (all weights)」，与 Design System 和原型保持一致。

**Minor gaps noted:**
- `accent` color (#2D3B8A) is underused — most headers use text-primary (#1A1A1A)
- No dark mode variables (acceptable for MVP, declared NOT in scope)

---

## Pass 6: Responsive & Accessibility — 3/10 → 6/10 → 8/10

### Decision 5: Contrast + Touch Targets (Run 1)
> **Question:** How much accessibility work should we spec?
>
> **Options considered:**
> - A) Fix contrast + touch targets + VoiceOver labels ← **SELECTED**
> - B) Full a11y spec
> - C) Defer to implementation
>
> **User chose: A — Fix contrast + touch targets**

**Specs Added:**
- **Contrast fix:** Change `text-tertiary` from #9CA3AF to #6B7280 (4.6:1, passes WCAG AA) ✅ Built
- **Touch targets:** All interactive elements ≥44×44pt ✅
- **VoiceOver labels:** Key actions labeled ("Home tab", timer readout, scan button, streak bar) ✅

---

### Decision 21: Defensive Dynamic Type Rules (Run 2)
> **Question:** iOS 用户中约 27% 使用非默认字体大小。目前设计系统使用固定像素值，完全没有考虑 Dynamic Type。虽然完整 Dynamic Type 支持延后到 v1.1，但 MVP 应该有防御性规则防止大字体时界面崩溃。
>
> **Options considered:**
> - A) 定义防御性 Dynamic Type 规则 ← **SELECTED**
> - B) 完全延后到 v1.1
>
> **User chose: A — 定义防御性 Dynamic Type 规则**

**Spec:**
- **最大缩放上限：** 120%（accessibilityMedium），超过此值不再放大
- **SwiftUI 实现：** `.dynamicTypeSize(...accessibilityMedium)`
- **溢出规则：**
  - Tab 标签：单行，超长 truncate（尾部省略）
  - 卡片标题：最多 2 行，lineLimit(2)
  - 按钮文字：单行，自动缩小至 minimumScaleFactor(0.8)
  - 聊天气泡：自适应高度，maxWidth 280px 不变
- **固定高度组件设 minHeight 而非 height：**
  - Tab Bar pill: minHeight 62px
  - Primary Button: minHeight 56px
  - Input Field: minHeight 48px
- **QA 测试规则：** 每个新页面必须在 Default 和 accessibilityMedium 两种设置下截图对比

---

## Pass 7: Unresolved Design Decisions — 9 Resolved, 0 Deferred

### Decision 6: Free vs Premium Visual Treatment (Run 1)
> **Question:** How to visually distinguish premium content from free content?
>
> **Options considered:**
> - A) Lock icon + "PRO" badge ← **SELECTED**
> - B) Blur + upgrade prompt
> - C) No distinction until limit hit
>
> **User chose: A — Lock icon + PRO badge**

**Spec:**
- Premium courses: Lock icon (16px, #9CA3AF) on thumbnail bottom-right + orange "PRO" pill badge top-right
- AI Chat limit: "3/5 messages today" counter in header. At limit: input disabled → "Upgrade" button
- Breed Scan limit: "0 scans left" + "Upgrade" link
- Tapping locked content: Mini paywall bottom sheet (not full-screen)

---

### Decision 7: Skip Behavior — Onboarding (Run 1)
> **Question:** Where does "Skip" on onboarding screens take the user?
>
> **Options considered:**
> - D) Skip slide → next slide
> - E) Skip all → Pet Setup ← **SELECTED**
> - F) Skip everything → Home
>
> **User chose: E — Skip all → Pet Setup (mandatory)**

**Spec:** "Skip" on any Welcome screen (1-3) jumps directly to Breed Photo Scan (Screen 4). Pet Setup is mandatory.

---

### Decision 22: Tab Bar Badges (Run 2)
> **Question:** Tab bar 没有徽章/红点来提示用户未读内容。HOME 有未完成任务、AI 有新建议、PROFILE 有新成就——但用户看不到，必须逐个点进去才知道。
>
> **Options considered:**
> - A) 定义品牌化 Tab 徽章规格 ← **SELECTED**
> - B) 使用标准 iOS 红点
>
> **User chose: A — 定义品牌化 Tab 徽章规格**

**Spec:**
- 位置：Tab 图标右上角，偏移 (x: +8px, y: -4px)
- 容器：minWidth 18px, height 18px, cornerRadius 999px
- 内边距：[2, 6]
- 背景：#FF7A3D (primary)，边框 2px solid #FFFFFF
- 字体：DM Sans, 10px, weight 700, #FFFFFF
- 数字规则：1-9 显示数字，10-99 显示数字，100+ 显示 "99+"，0 隐藏
- 触发规则：HOME = 未完成任务数, COURSES = 无徽章, AI = 新建议数, PROFILE = 新成就数 (72h 自动清除)
- 动画：出现 scale 0→1.2→1.0 (0.3s spring)，数字变化 scale bounce (0.15s)
- Active tab：徽章背景改 #FFFFFF，文字改 #FF7A3D（反色）

---

### Decision 23: Paywall Dual Visual Strategy (Run 2)
> **Question:** PRD 定义了两种付费墙（引导后软墙 + 锁定内容硬墙），但两种墙的视觉策略、信息层级、CTA 策略应该有所不同。软墙是「展示价值说服你」，硬墙是「你已经想要了，快付钱」。
>
> **Options considered:**
> - A) 区分两种付费墙视觉策略 ← **SELECTED**
> - B) 维持现有规格
>
> **User chose: A — 区分两种付费墙视觉策略**

**Spec:**

**软付费墙（全屏展示型 — Screen 8）：**
- 场景：引导流程完成后，用户尚未体验产品
- 心态：「这个 App 值得付费吗？」→ 需要说服
- 布局：品牌插图(40%) → 标题(H1) → 功能对比表(3-4行) → 3个价格方案(年度高亮) → "Start 7-Day Free Trial" CTA → "Continue Free" 文字按钮
- CTA 策略：强调试用，弱化跳过
- 退出：左上角 X 按钮

**硬付费墙（底部弹出型 — Mini Sheet）：**
- 场景：用户点击锁定内容
- 心态：「我想要这个功能」→ 已有意愿，快速转化
- 容器：底部 Sheet, 圆角顶部 20px, 最大高度 50%
- 布局：拖拽条 → 单句价值("Unlock all 60 courses") → 上下文(用户想访问的内容名+缩略图) → 仅年度方案(最佳性价比) → "Unlock Now" CTA → "See All Plans" 文字按钮(→跳转全屏软墙)
- CTA 策略：强调立即解锁，弱化比较

---

### Additional Specs Added (no user decision needed):
- **AI Chat typing indicator:** 3 animated dots in AI bubble, bounce animation 0.3s/dot, "Thinking harder..." after 8s
- **Multiple pets:** MVP single-pet only. Data model supports array for v1.1. No pet switcher in MVP.

---

## NOT in Scope (Explicitly Deferred)

| Item | Rationale |
|------|-----------|
| Dark mode | Not needed for MVP, color system supports it via variables |
| Full Dynamic Type support | MVP has defensive rules (max 120%), full support in v1.1 |
| Reduced motion preferences | Only confetti + shimmer spec'd, defer full support |
| iPad / larger screen layouts | iPhone-only MVP |
| Landscape orientation | Portrait-locked |
| Localization / RTL | English-only MVP |
| Pet switcher (multi-pet UI) | Data model supports it, UI deferred to v1.1 |
| Offline video playback | Technical complexity too high for MVP |
| Offline AI chat | Requires on-device LLM, not feasible for MVP |
| Advanced motion/transitions | 2-3 key animations spec'd, full motion system in v1.1 |

---

## What Already Exists (Reusable Assets)

| Resource | Status | How Design Uses It |
|----------|--------|--------------------|
| PawSmart Design System.md | Complete | All 23 decisions calibrated against it |
| 13 Pencil reusable components | Built | StatusBar, TabBar, Buttons, InputField, etc. |
| 17 color variables | Defined in prototype | Consistent token usage across all screens |
| 24 screens in pencil-new.pen | Built | 18 main + celebration modal + 5 empty states |
| PRD Sections 7.5-7.10 | Added via eng review | Account system, offline, AI safety, subscription sync, performance, LLM cost |
| Eng Review (16 issues) | Complete | All architectural decisions inform design specs |

---

## Action Items

### Run 1 Action Items (All Built ✅)

| # | Item | Status |
|---|------|--------|
| 1 | 5 Empty State Screens | ✅ Built |
| 2 | AI Hub Redesign | ✅ Built |
| 3 | Celebration Modal | ✅ Built |
| 4 | Contrast Fix | ✅ Built |

### Run 2 Action Items (Design Specs — For Implementation)

| # | Item | Description |
|---|------|-------------|
| 5 | Login Screen | Add to prototype — Sign in with Apple + Email + Guest |
| 6 | Offline UX | Implement 3-tier offline indicators (green/yellow/red) |
| 7 | Warning Card Component | Build reusable component with 3 variants (Info/Warning/Urgent) |
| 8 | Subscription State UX | Implement 6 state transitions with appropriate feedback |
| 9 | Usage Indicators | Add remaining-count displays to AI Chat and Breed Scan |
| 10 | Skeleton Screens | Implement unified spec across 9 screens |
| 11 | Error States | Implement 6 error scenario UIs |
| 12 | Success States | Implement 5 success feedback patterns |
| 13 | Progress States | Implement 6 progress/loading patterns |
| 14 | Soft Upgrade Transition | 3-phase trial expiry flow |
| 15 | Day 2-7 Return Experience | Dynamic greeting + streak bar + growth data + AI recommendations |
| 16 | Pet Elements in Settings | Add pet context to Settings and Subscription pages |
| 17 | PRD Font Correction | Change Section 6.1 from SF Pro to DM Sans |
| 18 | Dynamic Type Defense | Implement max 120% scaling + overflow rules |
| 19 | Tab Bar Badges | Branded badge component with trigger rules |
| 20 | Paywall Dual Strategy | Differentiate soft (full-screen) vs hard (bottom sheet) paywalls |

---

## Final Score

| Metric | Run 1 | Run 2 | Combined |
|--------|-------|-------|----------|
| Initial overall score | **7/10** | **6/10** (re-baselined) | — |
| Final overall score | **8/10** | **9/10** | **9/10** |
| Decisions made | 7 | 16 | **23** |
| Decisions deferred | 0 | 0 | **0** |
| Action items built | 4 | — | **4** |
| Action items for implementation | — | 16 | **16** |
| Items out of scope | 7 | 10 | **10** |
| Outside voices | — | Codex + Claude | ✅ |
| Lake Score | 7/7 | 16/16 | **23/23** |

---

*Run 1 completed: 2026-03-29*
*Run 2 completed: 2026-03-29*

---

## TODOS (Design Debt)

| # | TODO | Priority | Blocked By | 状态 |
|---|------|----------|------------|------|
| 1 | VoiceOver 无障碍标注规范 — 每个屏幕定义 accessibilityLabel/Hint | 开发前 | 无 | ✅ 已写入 Design System.md 第 10 节 |
| 2 | Dark Mode 设计令牌 — 17 个颜色变量的暗色模式映射 + 组件暗色状态 | 开发前 | 无 | ✅ 已写入 Design System.md 第 2 节 |
| 3 | 登录/注册屏幕原型 — Sign in with Apple + 邮箱登录，加入引导流程 | 开发前 | 无 | ✅ 已创建 pencil-new.pen Screen 3.5 |

---

## GSTACK REVIEW REPORT

| Review | Trigger | Why | Runs | Status | Findings |
|--------|---------|-----|------|--------|----------|
| CEO Review | `/plan-ceo-review` | Scope & strategy | 0 | — | — |
| Codex Review | `/codex review` | Independent 2nd opinion | 0 | — | — |
| Eng Review | `/plan-eng-review` | Architecture & tests (required) | 1 | CLEAR | 16 issues, 4 critical gaps |
| Design Review | `/plan-design-review` | UI/UX gaps | 1 | CLEAR | score: 6/10 → 9/10, 23 decisions |

- **UNRESOLVED:** 0 across all reviews
- **VERDICT:** ENG + DESIGN CLEARED — ready to implement
