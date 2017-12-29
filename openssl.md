```
https://www.openssl.org/docs/man1.1.0/apps/ciphers.html

openssl ciphers ${cipherspec} | sed 's/:/\n/g' | grep CBC

openssl ciphers HIGH | sed 's/:/\n/g' | grep -v CBC

openssl s_client -connect host:port -cipher MD5
openssl s_client -connect 172.16.127.134:443 -tls1


ssl_ciphers ECDHE-RSA-AES256-SHA:!ECDHE_RSA_AES_256_CBC_SHA:!DH:!EXPORT:!RC4:+HIGH:!MEDIUM:!LOW:!aNULL:!eNULL:@STRENGTH;


加密套件解读：
ECDHE-RSA-AES128-GCM-SHA256 为例

ECDHE：秘钥交换算法
RSA：签名算法
AES128：对称加密算法
GCM-SHA256：签名算法

默认项：
秘钥交换算法：RSA
签名算法：RSA
模式：CBC
AES256-SHA256 也就是 RSA-RSA-AES256-CBC-SHA256

优先级逻辑
    首先选择 ECDHE + AESGCM 密码。这些都是 TLS 1.2 密码并没有受到广泛支持。这些密码目前没有已知的攻击目标。
    PFS 密码套件是首选，ECDHE 第一，然后 DHE。
    AES 128 更胜 AES 256。有讨论是否 AES256 额外的安全是值得的成本，结果远不明显。目前，AES128 是首选的，因为它提供了良好的安全，似乎真的是快，更耐时机攻击。
    向后兼容的密码套件，AES 优先 3DES。暴力攻击 AES 在 TLS1.1 及以上，减轻和 TLS1.0 中难以实现。向后不兼容的密码套件，3DES 不存在.
    RC4 被完全移除. 3DES 用于向后兼容。
强制性的丢弃
    aNULL 包含未验证 diffie - hellman 密钥交换，受到中间人这个攻击
    eNULL 包含未加密密码(明文)
    EXPORT 被美国法律标记为遗留弱密码
    RC4 包含了密码，使用废弃ARCFOUR算法
    DES 包含了密码，使用弃用数据加密标准
    SSLv2 包含所有密码,在旧版本中定义SSL的标准,现在弃用
    MD5 包含所有的密码，使用过时的消息摘要5作为散列算法
    
```
