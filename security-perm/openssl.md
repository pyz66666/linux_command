# openssl

## 测试 HTTPS 服务并查看证书
```bash
openssl s_client -connect example.com:443 -servername example.com </dev/null 2>/dev/null | openssl x509 -noout -dates -subject -issuer
```
```
subject=CN = *.example.com
issuer=C = US, O = Let's Encrypt, CN = R11
notBefore=Jun 15 00:00:00 2026 GMT
notAfter=Sep 13 23:59:59 2026 GMT
```
> Let's Encrypt 签发的通配符证书（*.example.com），有效期 2026-06-15 至 2026-09-13。

## 查看完整证书链
```bash
openssl s_client -connect google.com:443 -showcerts </dev/null 2>/dev/null | grep -E "depth|Verification|Protocol|Cipher"
```
```
depth=2 C = US, O = Google Trust Services LLC, CN = GTS Root R1
depth=1 C = US, O = Google Trust Services LLC, CN = WR2
depth=0 CN = *.google.com
Verification: OK
Protocol  : TLSv1.3
Cipher    : TLS_AES_256_GCM_SHA384
```
> 证书链 3 级验证通过，使用 TLS 1.3 协议，AES-256-GCM 加密。

## 生成自签名证书
```bash
openssl req -x509 -newkey rsa:2048 -nodes -keyout key.pem -out cert.pem -days 365 -subj "/CN=localhost"
```
```
Generating a 2048 bit RSA private key
..........+++++
......................+++++
writing new private key to 'key.pem'
```
> 生成自签名证书和私钥，有效期 365 天，CN=localhost，仅适合测试环境。

## 计算文件 SHA256 哈希
```bash
openssl dgst -sha256 ubuntu-24.04.iso
```
```
SHA256(ubuntu-24.04.iso)= a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d607182930aabbccddeeff001122334455
```
> `dgst -sha256` 计算文件哈希，用于校验下载完整性。

## 生成安全随机字符串
```bash
openssl rand -base64 32
```
```
dGhpcyBpcyBhIHJhbmRvbSBzdHJpbmcgZ2VuZXJhdGVkIGJ5IG9wZW5zc2w=
```
> `rand -base64 32` 生成 32 字节随机数据并 Base64 编码，适合做密钥或令牌。

## 查看证书内容
```bash
openssl x509 -in cert.pem -noout -text | head -20
```
```
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            12:34:56:78:90:ab:cd:ef
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: CN = localhost
        Validity
            Not Before: Jul 12 10:35:42 2026 GMT
            Not After : Jul 12 10:35:42 2027 GMT
        Subject: CN = localhost
```
> `x509 -text` 显示证书全部字段：版本号、序列号、签名算法、有效期、主题等。
