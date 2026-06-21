# AGENTS.md

本文件面向 AI 编程助手，用于说明 `prostones.github.io` 项目的结构、技术栈、构建方式与开发约定。阅读者默认对项目一无所知。

## 项目概述

本项目是一个基于 [Hexo](https://hexo.io/) 7.x 的静态博客站点，使用 [NexT](https://theme-next.js.org/) 主题（Gemini 方案）。站点主要语言为中文（zh-CN），时区为 `Asia/Shanghai`，用于记录技术思考与生活点滴。

- **站点标题**：prostones
- **站点副标题**：记录技术与生活
- **部署目标**：GitHub Pages（仓库 `prostones/prostones.github.io`，分支 `master`）
- **主题版本**：NexT `^8.27.0`
- **Hexo 版本**：`^7.0.0`（`package.json` 中锁定的 Hexo 版本为 `7.3.0`）

## 技术栈

- **核心框架**：[Hexo](https://hexo.io/)（Node.js 静态站点生成器）
- **主题**：`hexo-theme-next`，使用 `Gemini` 方案并启用深色模式
- **模板渲染**：EJS（`hexo-renderer-ejs`）
- **Markdown 渲染**：[marked](https://marked.js.org/)（`hexo-renderer-marked`）
- **样式**：Stylus（`hexo-renderer-stylus`）
- **代码高亮**：highlight.js（Hexo 内置配置）
- **本地搜索**：`hexo-generator-searchdb`
- **字数统计**：`hexo-wordcount`
- **部署**：`hexo-deployer-git`

## 目录结构

```
.
├── _config.yml          # Hexo 主配置文件
├── _config.next.yml     # NexT 主题独立配置文件
├── package.json         # npm 依赖与脚本
├── package-lock.json    # npm 锁定文件
├── scaffolds/           # 新建文章/页面/草稿的模板
│   ├── draft.md
│   ├── page.md
│   └── post.md
└── source/              # 站点原始内容
    ├── _posts/          # 博客文章
    ├── about/           # 关于页面
    ├── categories/      # 分类列表页面
    └── tags/            # 标签列表页面
```

### 生成产物

Hexo 默认将构建结果输出到 `public/` 目录；`public/`、`node_modules/`、`.deploy_git/`、`db.json` 以及各种日志文件已加入 `.gitignore`，不应提交到版本控制。

## 构建与运行命令

项目使用 npm scripts 管理常用命令：

```bash
# 安装依赖
npm install

# 启动本地开发服务器（默认 http://localhost:4000）
npm run server

# 清理缓存与生成的 public 目录
npm run clean

# 生成静态站点
npm run build

# 部署到 GitHub Pages（master 分支）
npm run deploy
```

`npm run deploy` 会调用 `hexo-deployer-git`，将 `public/` 目录推送到 `_config.yml` 中配置的仓库与分支。执行前通常需要先运行 `npm run build`。

## 配置说明

### Hexo 主配置（`_config.yml`）

- 站点元数据：标题、副标题、描述、作者、语言、时区等。
- URL 与永久链接：`permalink: :year/:month/:day/:title/`
- 分页：每页 10 篇文章。
- 主题：显式指定 `theme: next`。
- 部署目标：

  ```yaml
  deploy:
    type: git
    repository: https://github.com/prostones/prostones.github.io.git
    branch: master
  ```

### NexT 主题配置（`_config.next.yml`）

- **方案**：Gemini
- **深色模式**：已启用
- **菜单**：home、about、tags、categories、archives，使用 Font Awesome 图标
- **侧边栏**：左侧显示
- **社交链接**：GitHub、Gitee、E-Mail
- **页脚**：自 2024 年开始
- **文章元信息**：显示创建时间、更新时间、分类
- **目录（TOC）**：启用，最大深度 6
- **本地搜索**：启用
- **代码块**：显示语言标识，提供复制按钮
- **阅读进度条**：顶部显示，颜色 `#37c6c0`
- **回到顶部**：启用，显示滚动百分比
- **知识共享协议**：CC BY-NC-SA，在侧边栏与文章中显示

## 内容组织与写作约定

### 文章（Posts）

- 文章源码存放在 `source/_posts/`。
- 使用 Markdown 格式，顶部必须包含 YAML Front-matter，例如：

  ```markdown
  ---
  title: 文章标题
  date: 2026-06-11 16:00:00
  tags:
    - Hexo
    - 博客
  categories:
    - 技术
  ---
  ```

- `tags` 与 `categories` 以 YAML 列表形式书写；`tags` 可包含多个，`categories` 可支持层级（列表嵌套）。

### 页面（Pages）

- 特殊页面以独立目录存放：
  - `source/about/index.md`：`type: about`
  - `source/categories/index.md`：站点分类列表页
  - `source/tags/index.md`：站点标签列表页

### 模板（Scaffolds）

- `scaffolds/post.md`：新建文章模板，包含 `title`、`date`、`tags`、`categories` 占位。
- `scaffolds/page.md`：新建页面模板。
- `scaffolds/draft.md`：新建草稿模板。
- 使用 `hexo new [layout] <title>` 创建内容时会读取对应模板。

## 代码风格与提交约定

- 项目本身不包含 ESLint、Prettier 或测试框架。
- Markdown 内容请保持中文排版习惯；技术术语可保留英文。
- 修改主题配置时，请优先编辑 `_config.next.yml`，不要直接修改 `node_modules/hexo-theme-next/_config.yml`。
- 修改站点全局行为（URL、分页、部署等）时，编辑 `_config.yml`。
- 不要提交 `public/`、`node_modules/`、`.deploy_git/`、`db.json`、日志文件或系统生成的 `.DS_Store`、`Thumbs.db`。

## 测试与部署

- **测试**：项目当前没有自动化测试。验证方式主要为本地运行 `npm run server` 并人工检查页面渲染、链接与样式。
- **部署流程**：
  1. `npm run clean`（可选，用于清除旧缓存）
  2. `npm run build`
  3. `npm run deploy`
- 部署依赖 Git 远程仓库权限；仓库地址已在 `_config.yml` 中硬编码。

## 依赖更新

仓库已启用 GitHub Dependabot（`.github/dependabot.yml`），每日检查 `/` 目录下的 npm 依赖更新，最多保持 20 个开放拉取请求。

## 安全注意事项

- `_config.yml` 中的仓库地址为公开 GitHub 仓库，无需在配置中存放凭证；但执行 `npm run deploy` 时需要本地 Git 凭证具备推送权限。
- 不要在任何 Markdown 文件、配置文件或 npm 脚本中写入密码、Token 或 SSH 私钥。
- 若启用评论、统计等第三方 NexT 插件，应单独审查其隐私与数据收集策略后再配置。

## 常用参考链接

- Hexo 文档：https://hexo.io/docs/
- NexT 文档：https://theme-next.js.org/docs/
- Hexo 配置参考：https://hexo.io/docs/configuration.html
