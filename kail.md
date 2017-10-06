vi /etc/ssh/sshd_config
PermitRootLogin yes
PasswordAuthentication yes

/etc/init.d/ssh restart

update-rc.d ssh enable





GRANT INSERT,DELETE,UPDATE,SELECT ON test.user TO 'foo'@'localhost';
flush privileges;


grant select,update on *.* to ljtest3@localhost identified by 'DBuser123!';
flush privileges;

show variables like '%password%';

select @@old_passwords;

set old_passwords=2;


select password(’123456′),length(password(’123456′));

SELECT @@session.old_passwords, @@global.old_passwords;
