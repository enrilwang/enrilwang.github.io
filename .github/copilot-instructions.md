<!--
为 AI 编码代理（例如 Copilot / 代码助手）提供可执行、项目特定的工作说明。
本文件基于仓库当前可见文件（仅 `README.md` 与 `LICENSE`）。
如果仓库后来添加了构建文件（如 `package.json` / `_config.yml` / `index.html` / `config.toml`），请先更新本文件。
-->

# Copilot 指令（项目特定指南）

本仓库目前只包含 `README.md` 与 `LICENSE`，尚未包含明显的构建/站点配置文件（例如 `package.json`, `_config.yml`, `index.html`, `_posts/`, `config.toml` 等）。因此，AI 代理在做出变更前应优先执行“识别/确认”步骤，而非直接假设使用 Jekyll、Hugo 或 Node 工具链。

**目标**：快速识别项目类型、列出可执行步骤、避免盲目修改，并在不确定时生成最小增量变更（PR + 说明）。

**快速检查清单（按优先级）**
- **存在性检查**：查看根目录是否含下列任一文件以判定构建工具：
  - `package.json` → Node/npm/webpack/Vite 等
  - `_config.yml` 或 `_posts/` → Jekyll
  - `config.toml` 或 `themes/` → Hugo
  - `index.html`、`404.html` → 可能为纯静态站点
  - `.github/workflows/*` → 查看 CI/CD 流程
- **如果都不存在**：把仓库视为“纯静态内容/空站点占位”，任何新增构建步骤必须在 PR 中说明理由。

**常用命令示例（基于发现的工具）**
- Node 项目：`npm install` 然后 `npm run build` 或 `npm start`（查 `package.json` 的 `scripts`）。
- Jekyll：`bundle install && bundle exec jekyll serve`（查 `_config.yml`）。
- Hugo：`hugo server`（查 `config.toml` / `config.yaml`）。
- 纯静态：本地可用 `python -m http.server` 或直接推送到 GitHub Pages（`main` 分支或 `gh-pages`）。

**PR / 修改策略（必须遵守）**
- 任何对站点构建/工具链的添加（例如新增 `package.json`、`Gemfile`、`_config.yml`）必须：
  1. 在 PR 描述顶部写明新增原因（例如“迁移到 Jekyll 以支持博客”）。
  2. 包含清晰的本地重现步骤和回退方案（如何还原到原始静态站点）。
 3. 如果引入新依赖，说明安全/许可考虑并在 PR 中列出这些依赖。
- 小改动（修正文案、添加图片、更新 README）可提交小型 PR，但应保持原有目录结构。

**代码/内容风格与约定（当前可见）**
- 仓库目前为极简结构 — 无特定代码风格约定可推断。提交信息使用简短说明（例如：`docs: update README`，`chore: add site scaffold`）。

**与外部系统的集成点**
- 没有发现 CI、CD 或第三方托管配置。
- 可能的集成点（如果后来添加）：GitHub Actions（`.github/workflows`）、Netlify（`netlify.toml`）、Vercel（`vercel.json`）。在实现这些集成前，先在 Issue 中征求仓库所有者批准。

**发现性示例**
- 当前 repo 路径示例：`/README.md`（存在）和 `LICENSE`（存在）。没有 `index.html`、`_config.yml`、`package.json` 或其他站点源文件 — 请据此先做探测而非直接假设构建工具。

**交互与提问模板（在不确定时使用）**
在创建 PR 之前，使用下列模板自动在 Issue/PR 描述中提醒维护者：

```
发现：仓库当前没有构建配置（`package.json` / `_config.yml` / `index.html`）。建议变更：<简述要做的事>。
问题：是否允许引入 <工具名>（例如 Jekyll / Hugo / Node）？
影响：会新增依赖并改变部署流程；提供回退方案：<说明回退步骤>。
```

---

如果你希望我直接起草一个最小的站点骨架（例如：`index.html` + `.github/workflows` 或 Jekyll 的 `_config.yml` + 示例页面），告诉我想要的工具链（纯静态 / Jekyll / Hugo / Vite），我会先在一个独立分支创建可回退的 PR 模板并附上运行说明。

--
最后：请告诉我是否需要把说明改为英文或补充 CI/部署细节。期待你的反馈以便迭代。 
