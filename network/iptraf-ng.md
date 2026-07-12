# iptraf-ng

## 监控指定接口的实时流量
```bash
sudo iptraf-ng -d eth0
```
```
┌──────────────────────────────────────────────────────────────┐
│                    IP Traffic Monitor                         │
│ Interface: eth0  (10.0.1.10)                                 │
│ Packets captured: 12845                                      │
├───────────────┬──────────────────┬───────────────────────────┤
│ Source        │ Destination      │ Protocol  Size    Rate     │
├───────────────┼──────────────────┼───────────────────────────┤
│ 10.0.1.10:443 │ 203.0.113.50:612 │ TCP      1420B   45.2Mbps │
│ 10.0.1.10:443 │ 198.51.100.20:49 │ TCP      1420B   38.1Mbps │
│ 10.0.1.10:22  │ 10.0.2.100:5423  │ TCP       64B    1.2Kbps  │
│ 10.0.1.10:53  │ 8.8.8.8:53       │ UDP       84B    0.5Kbps  │
│ 224.0.0.1     │ 10.0.1.10        │ IGMP      36B    0.1Kbps  │
├───────────────┴──────────────────┴───────────────────────────┤
│ TCP: 4 connections   UDP: 2 flows   ICMP: 0                  │
│ Incoming: 125.3 Mbps    Outgoing: 82.1 Mbps                  │
└──────────────────────────────────────────────────────────────┘
```
> `-d eth0` 显示该接口上每个活跃连接的实时协议、包大小和速率，入/出总带宽一目了然。

## 查看所有接口的通用统计
```bash
sudo iptraf-ng -g
```
```
┌───────────────────────────────────────────┐
│           General Interface Statistics     │
├──────────┬──────────┬──────────┬──────────┤
│ Iface    │  PktsIn  │  PktsOut │  Rate    │
├──────────┼──────────┼──────────┼──────────┤
│ lo       │     1234 │     1234 │   0 Kbps │
│ eth0     │   128450 │    98765 │ 125 Mbps │
│ docker0  │     5678 │     4321 │ 1.2 Mbps │
└──────────┴──────────┴──────────┴──────────┘
```
> `-g` 汇总各接口的收发包数，快速定位哪个网卡流量异常，比 `ip -s link` 更直观。

## 交互式全屏监控
```bash
sudo iptraf-ng
```
> 启动后进入 TUI 菜单界面，可动态选择 IP 流量监控、LAN 统计、按包大小分布等子功能。

## 后台批处理记录日志
```bash
sudo iptraf-ng -i eth0 -B -t 10 -L /var/log/iptraf.log
```
```
IPTraf-ng: Background mode enabled, logging to /var/log/iptraf.log
IPTraf-ng: Will run for 10 minutes and exit automatically
```
> `-B` 后台批处理、`-t 10` 运行 10 分钟后自动退出、`-L` 将数据写入日志文件，适合定时监控脚本。
