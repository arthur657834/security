Network Vulnerability Tests (NVTs)<br>
Greenbone Security Assistant (GSA)<br>

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

systemctl status openvas-manager
systemctl status openvas-scanner
systemctl status gsad

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

### 加载plugins并启动openvas-scaner服务
openvassd                                 

### 同步漏洞库
greenbone-nvt-sync

### 同步数据
greenbone-scapdata-sync<br>
greenbone-certdata-sync<br>
systemctl start openvas-scanner.service

### v9 漏洞库自动更新
```
[root@65-scan ~]# openvas-setup

Openvas Setup, Version: 3.0


Step 1: Update NVT, CERT, and SCAP data
Please note this step could take some time.
Once completed, this will be updated automatically every 24 hours
```

```
问题1:
ERROR: The number of NVTs in the OpenVAS Manager database is too low.

解决办法:
openvassd
openvasmd --rebuild --progress -v
```
