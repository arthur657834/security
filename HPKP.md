```
https://bsi.baidu.com/topic/https/hpkp.html
https://linux.cn/article-5282-1.html

HPKP作用:
互联网的信任机制完全依赖于CA（证书颁发机构）厂商颁发的证书，而任意一个CA厂商都可以签发任意一个域名的证书，导致攻击者可以从CA厂商（可以参考CA厂商入侵史）开始入手。因此需要使用白名单的方式来选择信任的CA，公钥扎钉public key pinning技术的出现，可以允许你强制指定签发证书的CA，只有指定的CA为你的域名签发的证书才能使用。

目前该技术有三种实现方式，DANE（基于DNSSEC）、HTTP公钥扎钉和TACK（证书密钥可信保证），HTTP公钥钉扎是使用最多的。
```
    
