# ip

## 查看所有网络接口的 IP 地址
```bash
ip addr show
```
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP
    link/ether 52:54:00:12:34:56 brd ff:ff:ff:ff:ff:ff
    inet 10.0.1.10/24 brd 10.0.1.255 scope global eth0
```
> `UP,LOWER_UP` 表示网卡已启用且物理链路接通，`inet 10.0.1.10/24` 是 IPv4 地址和子网掩码。

## 查看路由表
```bash
ip route show
```
```
default via 10.0.1.1 dev eth0
10.0.1.0/24 dev eth0 proto kernel scope link src 10.0.1.10
172.17.0.0/16 dev docker0 proto kernel scope link src 172.17.0.1
```
> 第一行 `default via 10.0.1.1` 是默认网关，第二行是直连路由，第三行是 Docker 自动添加的网桥路由。

## 查看 ARP 缓存表
```bash
ip neigh show
```
```
10.0.1.1 dev eth0 lladdr 00:1a:2b:3c:4d:5e REACHABLE
10.0.1.50 dev eth0 lladdr 52:54:00:12:34:56 STALE
10.0.1.100 dev eth0 lladdr 08:00:27:ab:cd:ef DELAY
```
> `REACHABLE` 表示 ARP 条目新鲜可用，`STALE` 表示已过期但还能用，`DELAY` 表示正在等待确认。

## 开启/关闭网卡
```bash
sudo ip link set eth1 down
sudo ip link set eth1 up
```
> 无输出即成功。`down` 禁用网卡，`up` 重新启用，比 `ifconfig eth1 down/up` 更快。

## 查看网卡流量统计
```bash
ip -s link show eth0
```
```
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP
    link/ether 52:54:00:12:34:56 brd ff:ff:ff:ff:ff:ff
    RX:  bytes    packets  errors  dropped  missed   mcast
        5234567890 3456789  0       120      0        450
    TX:  bytes    packets  errors  dropped  carrier  collsns
        1234567890 1234567  0       0        0        0
```
> `-s` 显示收发字节、包数、错误数和丢包数，`dropped=120` 说明接收队列丢弃了 120 个包需关注。

## 临时添加 IP 地址
```bash
sudo ip addr add 192.168.100.10/24 dev eth0
```
> 无输出即成功。该 IP 临时生效，重启后丢失，永久配置需写入网络配置文件。
