---
title: 建站日记 - 从零搭建 Hexo 博客
date: 2026-06-11 16:49:35
tags:
  - Hexo
  - NexT
  - Gitee
categories:
  - 技术
---

花了一点时间，用 Hexo 把个人博客搭起来了。

## 选型

- **框架**: Hexo — 基于 Node.js 的静态博客生成器，简洁高效
- **主题**: NexT (Gemini scheme) — 经典优雅，支持暗色模式、本地搜索
- **托管**: Gitee Pages — 国内访问速度快，稳定免费

## 搭建过程

Hexo 的初始化非常简单，一条命令就能生成项目骨架。主题选择 NexT 是因为它的生态比较完善，配置项丰富但上手不难。

整个流程：

1. `hexo init` 初始化项目
2. 安装 `hexo-theme-next` 主题和 `hexo-deployer-git` 部署插件
3. 配置 `_config.yml` 站点信息和部署地址
4. 配置 `_config.next.yml` 开启暗色模式、本地搜索、阅读进度条等功能
5. 创建"关于我"、"分类"、"标签"页面
6. 写第一篇文章
7. `hexo clean && hexo g && hexo d` 部署到 Gitee Pages

## 部署要点

Gitee Pages 有一个特别之处：仓库名必须严格遵循 `用户名.gitee.io` 的格式。部署后需要去 Gitee 仓库的"服务 → Gitee Pages"手动点击更新按钮（除非开通了 Pro 账户）。

## 后续计划

- 完善"关于我"页面
- 配置评论系统
- 持续写文章，积累内容
- 自定义主题样式

---

网站已上线：[https://prostones.gitee.io](https://prostones.gitee.io)
