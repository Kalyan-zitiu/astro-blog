# Kalyan Cyber Blog

一个基于 Astro 的个人博客与引导页。首页包含赛博朋克暗色视觉、动态粒子背景、Kalyan 立体 Logo、社交入口、博客分类悬浮菜单，以及生活 / 技术 / 工作三类文章筛选。

## 技术栈

- Astro 6
- Astro Content Collections
- Markdown 文章
- 原生 CSS 动效与少量浏览器脚本

## 本地运行

```sh
npm install
npm run dev
```

开发服务默认运行在 `http://localhost:4321`。

常用命令：

| 命令 | 作用 |
| --- | --- |
| `npm run dev` | 启动本地开发服务 |
| `npm run build` | 构建生产版本到 `dist/` |
| `npm run preview` | 本地预览生产构建 |
| `npm run astro -- --help` | 查看 Astro CLI 帮助 |

## 如何发布文章

文章放在 `src/content/blog/`。新增一篇文章时，创建一个新的 `.md` 文件，例如：

```text
src/content/blog/my-new-post.md
```

文件开头必须写 frontmatter：

```md
---
title: "文章标题"
description: "文章摘要，会显示在首页卡片和详情页顶部。"
pubDate: 2026-05-12
category: "tech"
tags: ["Astro", "博客", "前端"]
featured: false
draft: false
accent: "cyan"
---

这里开始写正文。
```

字段说明：

| 字段 | 必填 | 说明 |
| --- | --- | --- |
| `title` | 是 | 文章标题 |
| `description` | 是 | 文章摘要 |
| `pubDate` | 是 | 发布日期，建议使用 `YYYY-MM-DD` |
| `category` | 是 | 只能填 `life`、`tech`、`work` |
| `tags` | 否 | 标签数组 |
| `featured` | 否 | 是否作为首页精选文章 |
| `draft` | 否 | 为 `true` 时不会发布 |
| `accent` | 否 | 卡片强调色，可填 `cyan`、`magenta`、`amber`、`green` |

分类对应关系：

| 值 | 页面显示 |
| --- | --- |
| `life` | 生活 |
| `tech` | 技术 |
| `work` | 工作 |

保存文章后，首页会自动读取并按日期排序。运行 `npm run build` 可以检查字段是否填写正确。

## 修改链接和文案

首页入口都在 `src/pages/index.astro`：

- 邮箱：搜索 `mailto:hello@kalyan.dev`
- TikTok：搜索 `https://www.tiktok.com/@kalyan`
- 微信：搜索 `kalyan-wechat`
- 简历：默认链接为 `/resume/`，页面文件在 `src/pages/resume.astro`
- GitHub：搜索 `https://github.com/kalyan`
- Logo 名称：搜索 `Kalyan`

## 页面结构

```text
src/
├── components/
│   └── ParticleField.astro
├── content/
│   └── blog/
│       └── *.md
├── content.config.ts
├── layouts/
│   └── Layout.astro
└── pages/
    ├── index.astro
    └── blog/
        └── [...slug].astro
```

## 部署

先构建：

```sh
npm run build
```

构建产物会输出到 `dist/`。可以部署到 Vercel、Netlify、Cloudflare Pages 或任何支持静态站点的平台。

Vercel 设置参考：

- Framework Preset: `Astro`
- Build Command: `npm run build`
- Output Directory: `dist`
- Node.js: `>=22.12.0`

## GitHub 到 Vercel

上传到 GitHub 前建议先检查：

```sh
npm run build
git status
```

首次推送仓库的一般流程：

```sh
git add .
git commit -m "Build Kalyan cyber blog"
git branch -M main
git remote add origin https://github.com/<your-name>/<repo-name>.git
git push -u origin main
```

推送完成后，在 Vercel 里选择 `Add New Project`，导入这个 GitHub 仓库。Vercel 会识别 Astro；如果需要手动填写，使用上面的 Build Command 和 Output Directory。

后续更新文章或页面：

```sh
git add .
git commit -m "Update blog"
git push
```

Vercel 连接 GitHub 后，每次 push 到生产分支都会自动重新部署。
