---
title: nginx配置https服务器
date: 2018-03-15 20:08:14
tags:
	- https
	- nginx
---

## 写在前面

	最近自己搞了个服务器搭建了博客，也需要配上https啊，不能落伍了。
	nginx配置比较简单，略过。
	有免费的SSL证书let's encrypt，我们可以借此搭建个https的服务。

## 配置环境和准备
	你需要先申请一个域名。便宜点的几块钱一个。建议使用阿里云申请域名，然后做个实名认证。
	先把博客搭建好，能正常访问，然后再做https的配置。
	
	centOS 7，linux或者其它环境需要酌情修改。不一定适用。
	
	如果nginx占用了80端口，需要先service stop 一下，安装配置完毕之后再重启。
	

## 免费搭建权威机构颁发的https证书(推荐)

### 申请证书
```bash
curl https://get.acme.sh | sh
source ~/.bashrc
```
	acme.sh强大之处在于，可以自动配置DNS，不用去域名后台操作解析记录了，我的域名是在阿里注册的，下面给出阿里云解析的例子，
	其他地方注册的请参考这里自行修改：https://github.com/Neilpang/acme.sh/wiki/How-to-issue-a-cert
	
	网络上的教程基本上都是使用certbot，acme.sh比certbot的方式更加自动化，省去了手动去域名后台改DNS记录的步骤，而且不用依赖Python。
	推荐大家使用。
```bash
# 替换成从阿里云后台获取的密钥
export Ali_Key="xxxx"
export Ali_Secret="xxxx"
# 换成自己的域名
acme.sh --issue --dns dns_ali -d zengxiaowen.me -d *.zengxiaowen.me

#这里是通过线程休眠120秒等待DNS生效的方式，所以需要至少需要等待两分钟
```
	可以看到如下所示，申请成功。如果申请不成功可以多试几次。如果域名刚申请或者修改过DNS，一般需要申请几次才能成功。亲测。
![](/image/https_cert_verify.png)

### 配置nginx的conf

```buildoutcfg
	server {
			#listen       80; 配置了ssl，可以重定向到https，不开80端口。
			server_name  www.zengxiaowen.me;
			# force redirect http to https
			rewrite ^(.*) https://$server_name$1 permanent;
		
			listen 443 ssl;
			ssl_certificate /root/.acme.sh/zengxiaowen.me/fullchain.cer;
			ssl_certificate_key /root/.acme.sh/zengxiaowen.me/zengxiaowen.me.key;
			keepalive_timeout   70;
		}
```
	

## 使用openssl搭建非权威机构颁发的证书的https
	此种方式申请的证书会有不安全的标识。因为不是权威机构颁发的证书，是自己签发的。不推荐使用。

### 使用openssl步骤(不推荐)
```bash
sudo mkdir /etc/nginx/ssl
sudo openssl req -x509 -nodes -days 36500 -newkey rsa:2048 -keyout /etc/nginx/ssl/nginx.key -out /etc/nginx/ssl/nginx.crt
cd /etc/nginx/conf.d
cp default.conf default.conf.origin
vi default.conf

```
### 修改配置的内容

```buildoutcfg
	server {
		listen       80;  #remove this line if you want to disable http
		server_name  www.zengxiaowen.me;
		rewrite ^ https://$http_host$request_uri? permanent;    # force redirect http to https
	
		listen 443 ssl;
		ssl_certificate /etc/nginx/ssl/nginx.crt;
		ssl_certificate_key /etc/nginx/ssl/nginx.key;
		keepalive_timeout   70;
	
		fastcgi_param   HTTPS               on;
		fastcgi_param   HTTP_SCHEME         https;
	}

```
