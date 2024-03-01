---
title: Cloudflare 重定向的次数过多的解决方法
categories:
  - - 经验分享
    - 运维
tags:
  - - 运维
  - - CloudFlare
abbrlink: b62940d6
recommend: true
cover: 'https://p.wzsco.top/e32d80d346462627a8b0630016b74c7b.png/cover'
date: 2023-07-01 00:00:00
---
## Nginx 强制跳转 HTTPS 配置无误且使用了 Cloudflare 后出现 ERR_TOO_MANY_REDIRECTS 301 将您重定向的次数过多的解决方法

新项目初始因为用的是 Cloudflare 的 DNS 解析，下意识的开启了 CDN，在这之后才开始配置 Nginx，明明配置的没问题但是 HTTP 强制跳转 HTTPS 就是会报 ERR_TOO_MANY_REDIRECTS 301 将您重定向的次数过多的错误，百思不得其解。
后来在查询解决方案的时候试着加上了 Cloudflare 关键词，然后看到了这篇文章：一种可能导致 ERR_TOO_MANY_REDIRECTS 的原因，感觉就是这个原因，试了下果然解决了，优化下标题 SEO 希望能给更多人看到。
虽然很简单还是放下具体的操作步骤。

------

1. 确定你的 Nginx 配置是没有问题的。
   ```yaml
      # HTTP 80 端口
      server {
             listen      80;
             server_name example.com;
             root        /usr/share/nginx/html;
             index       index.html;
      
             # 强制跳转 HTTPS
             location / {
                 return 301 https://$server_name$request_uri;
             }
         }
      
      # HTTPS 443 端口
      server {
             listen      443 ssl;
             server_name example.com;
             root        /usr/share/nginx/html;
             index       index.html;
      
             # SSL 配置
             ssl_certificate             /etc/letsencrypt/live/example.com/fullchain.pem;
             ssl_certificate_key         /etc/letsencrypt/live/example.com/privkey.pem;
             ssl_protocols               TLSv1 TLSv1.1 TLSv1.2;
             ssl_ciphers                 ECDHE-RSA-AES128-GCM-SHA256:HIGH:!aNULL:!MD5:!RC4:!DHE;
      
             location / {
                 # 服务所在端口
                 proxy_pass http://127.0.0.1:8080;
                 proxy_http_version 1.1;
                 proxy_set_header Upgrade $http_upgrade;
                 proxy_set_header Connection "upgrade";
                 proxy_set_header Host $host;
             }
         }
   ```
   这样的配置至少 HTTP 强制跳转 HTTPS 就已经是没有问题的了，在防火墙和安全组打开 80 和 443 端口之后不会出现重定向不到的问题。
   修改完记得重启 Nginx 服务。
   ```shell
   nginx -s reload
   service nginx restart
   ```
2. Cloudflare 配置修改 SSL/TLS 为端到端加密。
   原因在开头文章中已经讲的很明确了：
> **原因**
> 因为在 Cloudflare 的 SSL/TLS 设置选项中，如果你选择了 Flexible ，那么所有对你的服务器的请求都是通过 HTTP 发送的，而如果服务器上已经设置了将 HTTP 重定向到 HTTPS 的话，就会发生重定向循环。