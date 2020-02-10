---
title: 使用 Hexo 搭建 Github Page
date: 2019-10-29 0:13:29
tags: 
---

介绍了本博客网页搭建的基本过程

<!-- more -->

## 准备工作

1. [Node.js](https://nodejs.org/)

2. [Git](https://git-scm.com/)

   以下以 `$` 开头的指令都表示在 Git Bash 中输入。Bash中可以使用 Ctrl+Ins 复制、使用 Shift+Ins 粘贴。

3. Hexo

   安装：
   
   ```
   $ npm install -g hexo-cli --save
   ```
   
   初始化（先定位到你想保存博客内容的地方）：
   
   ```
   $ hexo init
   $ npm install
   ```

4. Repository

   新建一个代码仓库，命名**必须为** `<username>.github.io` ，其中 `<username>` 为Github用户名。

5. 发布

   安装插件
   
   ```
   $ npm install hexo-deployer-git --save
   ```
   
   修改根目录下的 `_config.yml` 文件
   
   ```
   # Deployment
   ## Docs: https://hexo.io/docs/deployment.html
   deploy:
     type: git
     repo: git@github.com:<username>/<username>.github.io
     branch: master
   ```
   
   其中 `<username>` 为 Github 用户名。

## 博客写作流程

### 添加文章

```
hexo n <artical name>
```

其中 `<artical name>` 为文章将来的子链接

### 生成

```
hexo g
```

### 预览

```
hexo s
```

此时可通过 `http://localhost:4000/` 预览博客内容

### 部署

```
hexo d
```

部署到远程服务器以完成整个博客网站的发布或更新。

## 个性化

### 更换主题

找到主题对应的repo链接，然后克隆到 `themes/` 文件夹下，然后修改根目录下的 `_config.yml` 文件，将 `theme:` 字段设为对应的主题名即可。

比如 [NexT](http://theme-next.iissnan.com/) 主题，则在Git Bash中输入

```
git clone https://github.com/theme-next/hexo-theme-next themes/next
```

然后将 `theme:` 字段设为 `next` 。

### 更换语言

修改根目录下的 `_config.yml` 文件，将 `language:` 字段设为 `zh-CN` ，即可将网站改为中文。

### 主题个性化

按照官方文档修改主题目录下 `_config.yml` 文件的对应字段即可。

### 解决 NexT 主题下渲染 LaTeX 失败的问题

1. 开启 MathJax

   修改根目录下 `_config.yml` 文件的 `math:` 相关字段

2. 更换 Markdown 渲染引擎

   ```
   npm uninstall hexo-renderer-marked --save
   npm install hexo-renderer-kramed --save
   ```

3. 修改 `node_modules/kramed/lib/rules/inline.js` 文件，做以下替换：

   ```
   //escape: /^\\([\\`*{}\[\]()#$+\-.!_>])/,
   escape: /^\\([`*\[\]()#$+\-.!_>])/,
   //em: /^\b_((?:__|[\s\S])+?)_\b|^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,
   em: /^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,
   ```

### 绑定域名

这里以[阿里云](https://wanwang.aliyun.com/)为例。购买好域名后，在控制台中为域名增加两条解析记录：

| 主机记录 | 记录类型 | 解析线路(isp) |         记录值         |
| :------: | :------: | :-----------: | :--------------------: |
|   www    |  CNAME   |     默认      | `<username>.github.io` |
|    @     |  CNAME   |     默认      | `<username>.github.io` |

然后通过repo的setting选项，在custom domain中填写域名。

最后在 `source` 文件夹下添加文件 `CNAME` ，内容为域名。生成、部署后即可完成域名绑定。