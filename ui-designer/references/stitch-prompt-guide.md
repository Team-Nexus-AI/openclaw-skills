# Stitch Prompt 构建指南

Google Stitch 基于 Gemini 2.5 Pro，高质量 Prompt 能显著提升生成效果。

## Prompt 结构模板

```
A [platform] [page-type] for [app-description].

Layout: [layout description]

Components:
- [component 1 with details]
- [component 2 with details]
- [component N with details]

Style: [visual style, color scheme, typography]
Theme: [light/dark/system]
```

## 平台关键词

| 场景 | 关键词 |
|------|--------|
| 移动端 | `mobile-first`, `iOS-style`, `Android Material` |
| 桌面端 | `desktop web app`, `dashboard layout` |
| 响应式 | `responsive layout` |

## 风格关键词

| 风格 | 关键词 |
|------|--------|
| 现代简洁 | `clean modern design`, `minimal`, `whitespace-heavy` |
| 专业商务 | `professional`, `enterprise`, `corporate` |
| 暗黑模式 | `dark mode`, `dark theme`, `deep background` |
| 科技感 | `tech-forward`, `electric blue accent`, `neon` |
| 温暖亲和 | `warm tones`, `friendly`, `rounded corners` |

## 高分 Prompt 示例

### 登录页（移动端，暗黑）
```
A mobile login screen for a productivity app.

Layout: centered card on dark background, logo at top, form below

Components:
- App logo with name "TaskFlow" (centered, top)
- Email input field with icon
- Password input field with show/hide toggle
- "Remember me" checkbox
- "Sign In" primary button (full width, blue)
- "Forgot Password?" text link
- Divider with "or continue with"
- Google OAuth button (outlined)
- "Don't have an account? Sign Up" footer link

Style: dark mode, deep navy background (#0F172A), electric blue accent (#3B82F6), Inter font, rounded-xl components
```

### Dashboard（桌面端）
```
A desktop analytics dashboard for a SaaS admin panel.

Layout: left sidebar (240px) + main content area

Components:
- Sidebar: logo, nav items (Dashboard, Users, Analytics, Settings) with icons, user profile at bottom
- Top bar: page title, search input, notification bell, user avatar
- Stats row: 4 KPI cards (Total Users, MRR, Churn Rate, Active Sessions) with trend arrows
- Line chart: "Monthly Revenue" (last 6 months)
- Data table: recent transactions with columns (User, Amount, Status, Date), pagination

Style: light mode, white cards with subtle shadow, indigo primary (#4F46E5), gray-50 background, clean sans-serif
```

## 迭代 Prompt 技巧

生成后可用自然语言迭代，Stitch 上下文理解能力强：

- `"Change the primary color to [color], apply it to buttons and active states"`
- `"Make the layout more spacious, increase padding between sections"`
- `"Add a loading skeleton state for the data table"`
- `"Switch to dark mode while keeping the same layout"`

## 注意事项

- 描述越具体，生成质量越高（指定颜色值 > 描述颜色感觉）
- 指定字体和圆角大小能显著提升一致性
- 一次生成一个页面，不要在单个 Prompt 里要求多个页面
- 复杂 B 端页面（多层级数据表格）质量一般，需要人工调整
