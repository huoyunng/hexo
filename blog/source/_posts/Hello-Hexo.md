---
title: Hello Hexo
date: 2019-12-03 11:39:31
tags: hexo,blog
---
Welcome to Hexo

## Quick Start

### mkdir blog

```bash
# 创建博客文件目录
$ mkdir blog

# 进入博客目录
$ cd blog

# 在blog内 进行Hexo框架初始化
$ hexo init

# 安装依赖包
$ cnpm install
```

### Run server

``` bash
$ hexo server
```

### Create a new post

```bash
$ hexo new "this is my first post"
```

### Generate static files

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

##### 提示: 可以用 hexo help查看hexo的常用命令
```bash
$ hexo --help
Usage: hexo <command>

Commands:
  clean     Remove generated files and cache.
  config    Get or set configurations.
  deploy    Deploy your website.
  generate  Generate static files.
  help      Get help on a command.
  init      Create a new Hexo folder.
  list      List the information of the site
  migrate   Migrate your site from other system to Hexo.
  new       Create a new post.
  publish   Moves a draft post from _drafts to _posts folder.
  render    Render files with renderer plugins.
  server    Start the server.
  version   Display version information.

Global Options:
  --config  Specify config file instead of using _config.yml
  --cwd     Specify the CWD
  --debug   Display all verbose messages in the terminal
  --draft   Display draft posts
  --safe    Disable all plugins and scripts
  --silent  Hide output on console
```