# 企业智能体系统 · 功能快照（静态站部署说明）

这个目录里的页面是**纯静态 HTML**：所有展示数据已经内嵌在页面里，不连接任何后端、不需要数据库、不需要 API Key、不需要云隧道。放到任何静态托管上都能打开，也不需要本机开机。

## 文件内容

| 文件 | 用途 |
|---|---|
| `index.html` | 展示页，根路径直达 |
| `showcase.html` | 同一份展示页，保留 `/showcase.html` 路径，方便沿用旧链接 |
| `real.css` | 页面样式（上面两个页面引用它） |
| `.nojekyll` | 让 GitHub Pages 跳过 Jekyll 处理 |
| `.github/workflows/pages.yml` | 可选的自动部署工作流（用了它就不用手动开 Pages 分支） |
| `../showcase-standalone.html` | 单文件版，样式已内联，单独发给别人双击也能看 |

## 页面内容

四个功能区块 + 系统状态卡，共 15 个可点选的运行实例，全部取自 2026-11-13 本机真实运行记录：

- **P1 知识库问答**：正常回答（带 3 条引用）、缓存命中、语料外问题证据不足拒答、过滤器空证据拒答、引用回链（原文 + 页码 + 版面定位）。
- **P2 多工具智能体**：食材 + 病症的禁忌推理（命中与未命中）、知识图谱规模。
- **P3 工作流编排**：完整流式输出、无食材时的降级路径。
- **P4 评测与压测**：分层评测 + 门禁结论（BLOCKED）、只读门禁快照、并发压测报告（QPS / P99 表格）、只读压测快照。

每个实例都标注了对应的真实接口、参数、HTTP 状态与本机耗时。评测报告里项目原文自带的 `pipeline_selfcheck` 口径说明原样保留，不把它当作系统质量结论。

## 方式 1：GitHub 网页上传（最省事，不用装工具）

1. 在 GitHub 新建一个 **Public** 空仓库（例如 `agent-system-showcase`），**不要**勾选初始化 README。
2. 打开仓库 → `Add file` → `Upload files`，把 `index.html`、`showcase.html`、`real.css` 三个文件拖进去（`.nojekyll` 可选），Commit changes。
3. `Settings` → `Pages` → `Build and deployment` → `Source` 选 **Deploy from a branch** → Branch 选 `main` / `root` → Save。
4. 等 1–2 分钟，访问：
   - `https://<用户名>.github.io/<仓库名>/`
   - `https://<用户名>.github.io/<仓库名>/showcase.html`

想用工作流自动部署：把 `.github/workflows/pages.yml` 一起上传，并在 `Settings` → `Pages` → `Source` 改选 **GitHub Actions**；以后每次 push 会自动更新。两种方式二选一即可。

命令行版本（把 `<用户名>`、`<仓库名>` 换成自己的，仓库需先在 GitHub 建好）：

```powershell
cd F:\study_work\portfolio-showcase\deploy-pages
git init
git add .
git commit -m "static showcase"
git branch -M main
git remote add origin https://github.com/<用户名>/<仓库名>.git
git push -u origin main
```

## 方式 2：Vercel（拖拽或导入 Git 仓库）

vercel.com → `Add New…` → `Project` → 选择已推到 GitHub 的仓库导入（或安装 CLI 后在本目录执行 `vercel --prod`）。纯静态项目无需构建：Framework Preset 选 `Other`，Build Command 与 Output Directory 都留空。部署完得到 `https://<项目名>.vercel.app/`。

## 方式 3：Netlify Drop（连仓库都不用建）

打开 https://app.netlify.com/drop ，把整个目录拖进去，立即得到一个可分享域名；登录后可在 `Site settings` 里改成固定子域名。

## 本机验证

直接双击 `index.html`（`file://` 也可打开），或者：

```bash
cd F:/study_work/portfolio-showcase/deploy-pages
python -m http.server 8080
# 浏览器打开 http://127.0.0.1:8080/
```

## 更新页面

重新采集运行记录并生成展示页后，把新的 `index.html` / `showcase.html` 覆盖进来再 push 一次即可。静态站与实时演示站互不影响：实时站走本机代理，静态站只依赖这两个 HTML。
