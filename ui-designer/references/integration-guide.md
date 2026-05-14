# UI 代码融合指南

将 Stitch 生成的 HTML/CSS/JS 融合到不同技术栈项目的具体操作。

## 技术栈识别

```bash
# 识别前端框架
cat package.json | grep -E '"react"|"vue"|"svelte"|"next"|"nuxt"|"vite"'

# 识别样式方案
ls src/ | grep -E 'tailwind|styles|css'
cat package.json | grep -E '"tailwind"|"@mui"|"antd"|"chakra"'
```

## React / Next.js 项目

### 文件放置
```
src/
  components/
    ui/
      GeneratedPage.tsx   ← 新增
  app/
    new-page/
      page.tsx            ← 新增路由页面
  styles/
    generated.css         ← 样式（若不用 Tailwind）
```

### 转换步骤
1. 将 HTML 结构转为 JSX（`class` → `className`，`for` → `htmlFor`）
2. 提取重复结构为子组件
3. 将内联样式转为 Tailwind 类（若项目使用 Tailwind）
4. 添加 TypeScript 类型定义（若使用 TS）
5. 在 `app/` 或 `pages/` 下创建路由入口

### 代码模板
```tsx
// src/app/new-page/page.tsx
import GeneratedPage from '@/components/ui/GeneratedPage'

export default function Page() {
  return <GeneratedPage />
}

// src/components/ui/GeneratedPage.tsx
export default function GeneratedPage() {
  return (
    // 转换后的 JSX
  )
}
```

## Vue 3 / Nuxt 项目

### 文件放置
```
src/
  components/
    GeneratedPage.vue     ← 新增
  pages/
    new-page.vue          ← 新增路由
  assets/
    generated.css         ← 样式
```

### 转换步骤
1. 将 HTML 放入 `<template>` 块
2. CSS 放入 `<style scoped>` 块
3. 将 `class` 属性用 `:class` 绑定动态状态
4. 在 `pages/` 下创建路由文件（Nuxt 自动路由）

### 代码模板
```vue
<template>
  <!-- Stitch 生成的 HTML -->
</template>

<script setup lang="ts">
// 响应式状态和逻辑
</script>

<style scoped>
/* Stitch 生成的 CSS */
</style>
```

## 纯 HTML/Vanilla JS 项目

直接将 Stitch 输出保存为新文件，调整相对路径：

```bash
# 保存到项目
cp stitch-output.html src/pages/new-page.html

# 提取 CSS
# 将 <style> 块内容移到 src/styles/new-page.css
# 添加 <link rel="stylesheet" href="../styles/new-page.css">
```

## 无前端代码的后端项目

在项目根目录创建 `ui/` 目录：

```
项目根/
  ui/
    index.html
    styles/
      main.css
    scripts/
      main.js
    README.md    ← 说明如何启动 UI 预览
```

## Tailwind CSS 转换技巧

Stitch 生成的内联 CSS → Tailwind 类的常用映射：

| CSS 属性 | Tailwind 等效 |
|----------|--------------|
| `display: flex; justify-content: center` | `flex justify-center` |
| `background-color: #1F2937` | `bg-gray-800` |
| `border-radius: 12px` | `rounded-xl` |
| `padding: 16px 24px` | `py-4 px-6` |
| `font-size: 14px; color: #6B7280` | `text-sm text-gray-500` |

## 组件库适配

### Ant Design (antd)
- 将 Stitch 的 button → `<Button type="primary">`
- input → `<Input placeholder="...">`
- table → `<Table dataSource={} columns={} />`

### Material UI (MUI)
- button → `<Button variant="contained">`
- input → `<TextField label="..." />`
- card → `<Card><CardContent>...</CardContent></Card>`

### Tailwind UI / shadcn
- 保留 Tailwind 类，替换为对应的 shadcn 组件
- `<Button>`, `<Input>`, `<Card>` 等直接可用

## 融合后检查清单

- [ ] 新文件已创建在正确目录
- [ ] 路由已配置（可在浏览器访问）
- [ ] 没有破坏现有页面（运行 `npm run dev` 验证）
- [ ] 样式没有全局污染（使用 scoped/module）
- [ ] TypeScript 无报错（若使用 TS）
- [ ] 已告知用户如何访问新页面
