### 安装
yum -y install lynis

### 扫描
lynis --check-all
grep -E "Suggestingon|Warning" /var/log/lynis.log

### 配置文件
/etc/lynis/default.prf

