### 安装redis
```
redis.conf 取消以下两行注释
unixsocket /tmp/redis.sock
unixsocketperm 700
```

### 安装openvas
```
yum install -y wget bzip2 texlive net-tools alien gnutls-utils
wget -q -O - https://www.atomicorp.com/installers/atomic | sh
yum install openvas -y

openvas-setup
openvas-check-setup --v9
```

### 创建认证
openvas-mkcert-client -n om -i

### Rebuild the OpenVAS database
openvasmd --rebuild --progress

### 启动
openvasmd

### web url
https://<IP-ADDRESS>:9392 and login.


### 创建user  
openvasmd --create-user=admin --role=Admin && openvasmd --user=admin --new-password=666666 

```
问题1:
ERROR: The number of NVTs in the OpenVAS Manager database is too low.

解决办法:
openvassd
openvasmd --rebuild --progress -v
```
