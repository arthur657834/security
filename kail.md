### 开启ssh
```
vi /etc/ssh/sshd_config
PermitRootLogin yes
PasswordAuthentication yes

/etc/init.d/ssh restart
update-rc.d ssh enable
```

### 配置IP
```
vi /etc/network/interfaces

auto eth0
iface eth0 inet static
address 10.1.50.28
netmask 255.255.255.0 
gateway 10.1.50.1

/etc/init.d/networking restart
```

### 配置DNS
```
vi /etc/resolv.conf 
```

### 时间设置
```
timedatectl list-timezones
timedatectl set-timezone "Asia/Shanghai" 
timedatectl set-time '16:10:40 2015-11-20'
timedatectl set-ntp true
```
