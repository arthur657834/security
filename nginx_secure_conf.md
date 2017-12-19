```
安全配置:
server_tokens off;
more_clear_input_headers Range;
add_header X-Frame-Options SAMEORIGIN;
add_header X-Content-Type-Options nosniff;
add_header X-XSS-Protection "1; mode=block";
#0 – 关闭对浏览器的 xss 防护
#1 – 开启 xss 防护
#1; mode=block – 开启 xss 防护并通知浏览器阻止而不是过滤用户注入的脚本。
#1; report=http://site.com/report – 这个只有 chrome 和 webkit 内核的浏览器支持，这种模式告诉浏览器当发现疑似 xss 攻击的时候就将这部分数据 post 到指定地址。
add_header X-Download-Options noopen;
add_header Strict-Transport-Security "max-age=31536000; includeSubDomains";
add_header Cache-Control "max-age=0, no-cache, no-store, must-revalidate";
add_header Content-Security-Policy "default-src 'self'; script-src 'self' 'unsafe-inline' 'unsafe-eval'; style-src 'self' 'unsafe-inline'; img-src 'self' data:";


# referer
set $referers_block 0;
referer_hash_bucket_size 512;
valid_referers none blocked 10.1.61.228;
if ($invalid_referer) {
   set $referers_block "${referers_block}1";
}
if ($request_uri !~* (YYRUM|buriedPoint|connect|openapi)) {
   set $referers_block "${referers_block}1";
}
if ($referers_block = "011") {
   return   403;
}

# origin
set $origin_block 0;
if ($http_origin) {
   set $origin_block "${origin_block}1";
}
if ($http_origin !~* "^(http://|https://)?10\.1\.61\.228(:[0-9]{2,5})?$") {
   set $origin_block "${origin_block}1";
}
if ($request_uri !~* (YYRUM|buriedPoint|connect|openapi)) {
   set $origin_block "${origin_block}1";
}
if ($origin_block = "0111") {
   return   403;
}

if ($request_method !~ ^(HEAD|GET|POST|PUT|DELETE|OPTIONS)$) {
   return   444;
}

设置httponly等
proxy_cookie_path / "/; httponly; secure; SameSite=Lax";
        
SSL配置：
ssl on;
ssl_dhparam /etc/nginx/dhparam.pem;#openssl dhparam -out dhparam.pem 2048 // 在 ssh 运行， openssl 生成 2048 位的密钥而不是当作参数写入 nginx.conf 文件。
ssl_certificate /etc/nginx/ssl/server.crt;
ssl_certificate_key /etc/nginx/ssl/server.key;
ssl_protocols  TLSv1 TLSv1.1 TLSv1.2; # 不支持 SSL，因为不安全
ssl_session_cache builtin:1000 shared:SSL:10m; # 后面都是优化性能的
ssl_session_timeout 10m;
ssl_prefer_server_ciphers on;
ssl_session_tickets on;
#ssl_ciphers EECDH+CHACHA20:EECDH+AES128:RSA+AES128:EECDH+AES256:RSA+AES256:EECDH+3DES:RSA+3DES:!MD5; # 禁用某些不安全的 ciphers
ssl_ciphers ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256:!DH:!EXPORT:!RC4:+HIGH:!MEDIUM:!LOW:!aNULL:!eNULL;

ssl_stapling on;
ssl_stapling_verify on;
ssl_trusted_certificate /etc/nginx/ssl/ca-bundles.pem;
#wget https://startssl.com/certs/ca.crt
#wget https://startssl.com/certs/sca.server1.crt
#cat ca.crt sca.server1.crt > ca-bundles.pem
#OCSP（Online Certificate Status Protocol）的中文翻译是在线证书状态协议，它是用来检查证书是否有效的。虽然证书一般是有效的，但也可能被撤销，这时就需要实时查询证书的状态，以确保它有效。这个查询如果让浏览器去做，就比较浪费时间，而 OCSP stapling 技术则是让服务器自己查出来，再把状态信息（无法伪造）返回给浏览器，以加快验证过程。
resolver 8.8.4.4 8.8.8.8 valid=300s;
resolver_timeout 10s;

强制跳转 HTTPS：
location / {
        set $redirect_to_https "${http_upgrade_insecure_requests}${https}";
        if ($redirect_to_https = "1") {
            add_header Vary Upgrade-Insecure-Requests;
            return 307 https://$host$request_uri;
        }
    }

echo QUIT | openssl s_client -servername www.keakon.net -connect

检测网站：
https://bsi.baidu.com/topic/https.html#/header
https://www.ssllabs.com/ssltest/index.html

开启http2
listen 443 ssl http2 fastopen=3 reuseport;

打开 Chrome 的 Developer Tools，翻到 Network 页，刷新一下，在 Name 那行点下右键，勾选 Protocol，可以看到已经变成 h2 了。

优化配置：
gzip on;
gzip_vary on;
gzip_http_version 1.0; # 对 HTTP 1.0 启用，据说 30% 的移动流量是 HTTP 1.0，还好我用联通
gzip_min_length 1000; # 太小的没必要压缩
gzip_comp_level 6; # 其实大于 0 都行，CPU 够用就设大点吧
gzip_disable msie6;
gzip_types text/plain text/html text/css application/json application/javascript application/x-javascript text/javascript text/xml application/xml application/rss+xml application/atom+xml;

sendfile on; # 因为主要是小文件，就不启用 aio 了
sendfile_max_chunk 512k; # 较大的文件不要一次全读取了，浪费内存
tcp_nopush on; # 对于 keepalive 连接，可以尽快发送响应
tcp_nodelay on; # 包填满了再发，与 sendfile 组合用

```   
