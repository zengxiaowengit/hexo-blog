---
title: centOS下oh-my-zsh安装
date: 2018-03-15 12:03:25
tags:
	- zsh
	- centOS
---

## 前言
	centOS下安装oh-my-zsh 和 autojump还没有那么顺利。
	整理下。以后用到。存之。

## 安装zsh
```bash
yum install zsh
```

## 安装autojump
```bash
#注意此处不是autojump. centOS需要其他支持。
yum install autojump-zsh
```
	
## 修改~/.zshrc
```bash
vi ~/.zshrc

#添加一行
alias j=autojump 

#修改plugins	
plugins=(
  git
  autojump
)

#退出文件，生效配置。
source ~/.zshrc

#初始化autojump.在bash下，不要在zsh下生效。
source /usr/share/autojump/autojump.bash on startup

```

## 安装问题排查
```bash
#查看安装路径
rpm -qa | grep autojump
rpm -ql autojump

#切换为默认bash
chsh -s /bin/bash

#初始化autojump
source /usr/share/autojump/autojump.bash on startup
```
    