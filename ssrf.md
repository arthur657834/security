
CSRF（Cross-site request forgery）跨站请求伪造，也被称为“One Click Attack”或者Session Riding，通常缩写为CSRF或者XSRF，是一种对网站的恶意利用。尽管听起来像跨站脚本（XSS），但它与XSS非常不同，XSS利用站点内的信任用户，而CSRF则通过伪装来自受信任用户的请求来利用受信任的网站。与XSS攻击相比，CSRF攻击往往不大流行（因此对其进行防范的资源也相当稀少）和难以防范，所以被认为比XSS更具危险性。

SSRF(Server-Side Request Forgery:服务器端请求伪造) 是一种由攻击者构造形成由服务端发起请求的一个安全漏洞。一般情况下，SSRF攻击的目标是从外网无法访问的内部系统。<br>
例: url分享

绕过方法
>http://www.baidu.com@10.10.10.10与http://10.10.10.10 请求是相同的

>ip地址转数字
>>10.1.50.250
每个数字转16进制数字，再将16进制数字转成10进制<br>
PING 167850746 (10.1.50.250) 56(84) bytes of data.<br>
64 bytes from 10.1.50.250: icmp_seq=1 ttl=64 time=0.160 ms<br>

>短地址

>xip.io
>>10.0.0.1.xip.io   resolves to   10.0.0.1<br>
>>www.10.0.0.1.xip.io   resolves to   10.0.0.1<br>
>>mysite.10.0.0.1.xip.io   resolves to   10.0.0.1<br>
>>foo.bar.10.0.0.1.xip.io   resolves to   10.0.0.1<br>
>>http://xip.io/<br>
