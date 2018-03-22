---
title: centOS一些常用命令和功能
date: 2018-03-16 10:43:46
tags:
	- centOS
---

##	crontab配置定时任务
	
	示例：
```bash
# 添加一个定时任务
crontab -e
# 添加一行。每隔一分钟执行从github更新博客的任务。
*/1 * * * * sudo /usr/share/nginx/html/zengxiaowengit.github.io/update.sh

#查看crontab执行日志
tail -f /var/log/cron
```

## 添加开机自动启动任务

	例如：开机自动启动nginx
```bash
vi /etc/rc.d/rc.local
#添加命令
service nginx start

```
