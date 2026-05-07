# 迭代法 Slidev 课件

一个基于 Slidev 制作的《算法设计与分析》课程课件，主题为“4.1 迭代算法”。

## 本地预览

```bash
npm install
npm run dev
```

默认预览地址：

```text
http://localhost:3030
```

## 构建静态页面

```bash
npm run build
```

构建完成后，静态文件会输出到 `dist/` 目录。

## 项目结构

- `slides.md`：主课件内容
- `style.css`：自定义样式
- `setup/main.ts`：全局样式与 Slidev 启动设置
- `public/`：静态资源

## 发布方式

这个项目可以直接部署到：

- GitHub Pages
- Vercel
- Netlify

仓库中已经包含：

- `vercel.json`
- `netlify.toml`
- `.github/workflows/deploy-pages.yml`

## 用 GitHub Pages 在线分享

把仓库推送到 GitHub 后，按下面设置一次即可：

1. 进入仓库 `Settings`
2. 打开 `Pages`
3. 在 `Build and deployment` 里选择 `GitHub Actions`
4. 保证默认分支是 `main`
5. 之后每次 `push` 到 `main`，GitHub 都会自动构建并发布

发布成功后，在线地址通常是：

```text
https://你的用户名.github.io/你的仓库名/
```

如果仓库名本身就是 `你的用户名.github.io`，那么地址就是：

```text
https://你的用户名.github.io/
```

## 技术栈

- Slidev
- Vue 3
- Markdown
- KaTeX / Shiki（由 Slidev 提供）
