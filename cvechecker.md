```
yum -y install mariadb mariadb-server cvechecker libxslt
systemctl start mariadb 
mysql_secure_installation

mysql -uroot -pljtest123
mysql>CREATE DATABASE cvechecker;
mysql>CREATE USER 'cvechecker'@'%' IDENTIFIED BY 'cvecheckpass';
mysql>GRANT ALL ON cvechecker.* TO 'cvechecker'@'localhost';
mysql>GRANT ALL ON cvechecker.* TO 'cvechecker'@'%';
mysql>FLUSH PRIVILEGES;

mysql -uroot -pljtest123 cvechecker <  /usr/share/cvechecker/mysql_cvechecker.sql

配置mysql
vi /etc/cvechecker.conf 

初始化
cvechecker -i

从cve网站拉数据
pullcves pull

find / -type f -perm -o+x > /tmp/cvecheck.tmp 
cat /proc/version >> /tmp/cvecheck.tmp
cvechecker -b /tmp/cvecheck.tmp

生成报告
cvechecker -r
```
