```
Install some library
# yum -y groupinstall "Development Tools"
# yum -y install libev libev-devel zlib zlib-devel openssl openssl-devel git
Install nghttp2
# cd /var/tmp
# git clone https://github.com/tatsuhiro-t/nghttp2.git
# cd nghttp2
# autoreconf -i
# automake
# autoconf
# ./configure
# make
# make install
Set library search path
# echo '/usr/local/lib' > /etc/ld.so.conf.d/custom-libs.conf
# ldconfig
# ldconfig -p| grep libnghttp2
 libnghttp2.so.14 (libc6,x86-64) => /usr/local/lib/libnghttp2.so.14
 libnghttp2.so (libc6,x86-64) => /usr/local/lib/libnghttp2.so
Install cURL
# cd /var/tmp
# git clone https://github.com/bagder/curl.git
# cd curl
# ./buildconf
# ./configure --with-nghttp2=/usr/local

Check it.
  HTTP2 support:    enabled (nghttp2)

# make
# make install
Check cURL Features. Does it have HTTP2?
# ./src/curl -V
curl 7.45.0-DEV (x86_64-unknown-linux-gnu) libcurl/7.45.0-DEV OpenSSL/1.0.1e zlib/1.2.7 nghttp2/1.3.1-DEV
Protocols: dict file ftp ftps gopher http https imap imaps pop3 pop3s rtsp smb smbs smtp smtps telnet tftp
Features: IPv6 Largefile NTLM NTLM_WB SSL libz HTTP2 UnixSockets
Check HTTP/2 response with Test URL.
# ./src/curl --http2 -v https://http2bin.org/get
```
