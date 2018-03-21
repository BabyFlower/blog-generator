---
title: hexo安装、github同步
date: 2018-03-21 12:26:00
tags:
---

**linux系统中需要提前安装有npm和git,并且配置了github的ssh**

# linux安装hexo
+ npm install -g hexo-cli，可能会提示权限不够，用
sudo执行即可
+ hexo -v 
+ 若提示hexo command not found，在PATH中添加hexo/bin的路径即可
+ 安装成功后，hexo init myBlog
+ 进入myBlog目录，cd myBlog
+ npm install
+ hexo new 文章名，新建一篇文章，成功后，显示该文章所在路径
+ 编辑myBlog中的_config.yml配置文件，title: 博客名，author: 作者名，type: git，添加repo: github仓库地址
**注意：repo:后面有空格**
+ npm install hexo-deploy-git --save,部署git插件
+ hexo deploy

# github关联hexo
+ 新建空repo仓库，仓库名称为 用户名.github.io
+ 开启仓库的GitHub Pages功能


# 后续编写博客流程
+ hexo new 文章名
+ 编辑文章
+ hexo generate
+ hexo deploy



