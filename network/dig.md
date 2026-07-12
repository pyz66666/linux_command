# dig

## 查询 A 记录
```bash
dig www.example.com
```
```
; <<>> DiG 9.18.0 <<>> www.example.com
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 12345
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; QUESTION SECTION:
;www.example.com.               IN      A

;; ANSWER SECTION:
www.example.com.        300     IN      A       93.184.216.34

;; Query time: 12 msec
;; SERVER: 192.168.1.1#53(192.168.1.1)
```
> `status: NOERROR` 表示查询成功，ANSWER SECTION 中 `300` 是 TTL（秒），`A` 记录返回 IPv4 地址。

## 简洁查询（仅显示结果）
```bash
dig +short www.example.com
```
```
93.184.216.34
```
> `+short` 只输出解析结果，干净无冗余，脚本中直接取值最方便。

## 查询 MX 记录（邮件服务器）
```bash
dig +short example.com MX
```
```
10 mail.example.com.
20 mail2.example.com.
```
> MX 记录前的数字（10, 20）是优先级，值越小越优先，邮件先投递到 `mail.example.com`。

## 使用指定 DNS 服务器查询
```bash
dig @8.8.8.8 www.example.com +short
```
```
93.184.216.34
```
> `@8.8.8.8` 指定用 Google DNS 查询，方便对比不同 DNS 服务器的解析结果是否一致。

## 反向解析 IP 到域名
```bash
dig -x 8.8.8.8 +short
```
```
dns.google.
```
> `-x` 进行 PTR 反向查询，将 IP 地址解析为域名。

## 追踪完整解析路径
```bash
dig +trace www.example.com
```
```
.                       518400  IN      NS      a.root-servers.net.
com.                    172800  IN      NS      a.gtld-servers.net.
example.com.            172800  IN      NS      a.iana-servers.net.
www.example.com.        86400   IN      A       93.184.216.34
```
> `+trace` 从根域名服务器开始逐级追踪，清晰展示 DNS 迭代查询的完整过程。
