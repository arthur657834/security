systemctl status auditd
```
auditctl -w /etc/passwd -p rwxa
* -w path : 指定要监控的路径，上面的命令指定了监控的文件路径 /etc/passwd
* -p : 指定触发审计的文件/目录的访问权限
* rwxa ： 指定的触发条件，r 读取权限，w 写入权限，x 执行权限，a 属性（attr）

auditctl -w /root/ljtest
auditctl -l 
ausearch -f /root/ljtest
aureport
```

/etc/audit/audit.rules 分三类:
* basic audit system parameters: 整体全局参数设置

* file and directory watches: 目录权限的设置以及是否可以查看某个目录或者文件

* system call audits: 系统调用的规则配置

ex:
```
#Record file permission changes 
-a entry,always -S chmod 
``` 
