title: hexo博客使用指南
tag: 
- hexo
---
Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

<!-- more -->

## 环境准备

-   node
-   npm
-   git

## Quick Start

### 使用npm安装hexo
``` bash
npm install hexo-cli -g
npm install hexo --save
hexo -v 
#正常执行说明安装成功
```

### hexo配置部署到github.io
    
    在_config.yml文件中，找到Deployment，然后按照如下修改：
    deploy:
      type: git
      repo: git@github.com:yourname/yourname.github.io.git
      branch: master

### hexo常用命令


``` bash
#Create a new post
hexo new "My New Post"

# 运行本地服务器
hexo server 
hexo s  #简化版。

# 生成静态文件
hexo generate
hexo g

# 部署到远程github
hexo deploy
hexo d
```

