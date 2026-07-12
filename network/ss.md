# ss

## 查看所有 TCP 监听端口
```bash
ss -tlnp
```
```
State    Recv-Q   Send-Q   Local Address:Port     Peer Address:Port   Process
LISTEN   0        128      0.0.0.0:22            0.0.0.0:*           users:(("sshd",pid=892,fd=3))
LISTEN   0        511      0.0.0.0:80            0.0.0.0:*           users:(("nginx",pid=1234,fd=6))
LISTEN   0        128      127.0.0.1:3306        0.0.0.0:*           users:(("mysqld",pid=1567,fd=21))
LISTEN   0        128      [::]:22               [::]:*              users:(("sshd",pid=892,fd=4))
```
> `-tlnp` 四合一：TCP、监听中、端口号、进程名，是排查"端口被谁占用"的最常用组合。

## 查看已建立的连接
```bash
ss -tnp state established
```
```
State   Recv-Q  Send-Q  Local Address:Port      Peer Address:Port       Process
ESTAB   0       0       10.0.1.10:22            10.0.2.100:54231       users:(("sshd",pid=3241,fd=4))
ESTAB   0       0       10.0.1.10:443           203.0.113.50:61234     users:(("nginx",pid=1235,fd=12))
ESTAB   0       0       10.0.1.10:443           198.51.100.20:49876    users:(("nginx",pid=1235,fd=15))
```
> `state established` 过滤出活跃连接，`Send-Q` 非零说明发送队列有积压。

## 查看统计摘要
```bash
ss -s
```
```
Total: 158
TCP:   45 (estab 12, closed 20, timewait 8, synrecv 0)

Transport Total     IP        IPv6
RAW       0         0         0
UDP       8         5         3
TCP       25        15        10
```
> `-s` 快速纵览各类连接数量，`timewait 8` 是正常现象，不代表问题。

## 查看监听指定端口的进程
```bash
ss -tlnp sport = :3306
```
```
State    Recv-Q   Send-Q   Local Address:Port     Peer Address:Port   Process
LISTEN   0        128      127.0.0.1:3306        0.0.0.0:*           users:(("mysqld",pid=1567,fd=21))
```
> `sport = :3306` 精确过滤源端口，比 `grep` 更快更准确，直接定位占用 3306 端口的进程。
