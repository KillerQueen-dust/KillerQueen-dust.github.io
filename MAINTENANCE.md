# 个人主页维护手册

项目已重构为可维护的 PRISM/Next.js 源码工程。仓库继续保留在 WSL 即可；
`KillerQueen-dust.github.io` 是 GitHub 用户主页要求的仓库名，不能随意改名。

## 修改个人信息

日常内容都在 `content/`，无需修改 React 代码：

| 内容 | 文件 |
| --- | --- |
| 姓名、简介、邮箱、社交链接、头像路径、页脚日期 | `content/config.toml` |
| 研究兴趣和首页板块 | `content/about.toml` |
| 个人简介正文 | `content/bio.md` |
| 新闻 | `content/news.toml` |
| 论文 | `content/publications.bib` |
| 教学、奖励、学术服务 | `content/teaching.toml`、`awards.toml`、`services.toml` |
| CV | `content/cv.md` |

头像为 `public/ganyu.jpg`；论文配图放入 `public/papers/`，并在对应 BibTeX
条目中填写 `preview = {图片文件名}`。修改公开内容后，同时更新
`content/config.toml` 中的 `last_updated`。

新增论文可从 Google Scholar、Zotero 等导出 BibTeX，再粘贴到
`content/publications.bib`。常用扩展字段为：`selected = {true}`（显示在首页）、
`preview`（配图）、`description`（简介）、`keywords` 和 `code`。

## 本地预览

WSL 已通过 NVM 安装 Node.js 22。首次拉取或依赖变化后运行：

```bash
nvm use
npm ci
```

日常编辑时运行：

```bash
npm run dev
```

用 Windows 浏览器打开 <http://localhost:3000/>。发布前执行：

```bash
npm run lint
npm run build
python3 -m http.server 4173 --bind 127.0.0.1 --directory out
```

再打开 <http://localhost:4173/>，检查构建后的最终版本；按 `Ctrl+C` 停止服务。

## 云端部署

本地检查通过后：

```bash
git status
git add -A
git commit -m "Update website content"
git push origin main
```

推送会自动触发 `.github/workflows/deploy.yml`，GitHub Actions 将安装依赖、
检查、构建并发布网站。可在仓库的 **Actions** 页面查看进度。

首次使用此流程时，确认 GitHub 仓库 **Settings → Pages → Build and
deployment → Source** 已选择 **GitHub Actions**。部署成功后访问
<https://killerqueen-dust.github.io/>；通常等待一两分钟并强制刷新即可看到更新。

不要提交 `node_modules/`、`.next/` 或 `out/`，它们都会由本地或云端自动生成。
