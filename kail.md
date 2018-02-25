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
```

### 配置DNS
```

```
