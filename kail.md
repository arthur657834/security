vi /etc/ssh/sshd_config
PermitRootLogin yes
PasswordAuthentication yes

/etc/init.d/ssh restart

update-rc.d ssh enable
