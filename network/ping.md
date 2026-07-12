# ping

## 测试连通性
```bash
ping -c 4 www.example.com
```
```
PING www.example.com (93.184.216.34) 56(84) bytes of data.
64 bytes from 93.184.216.34: icmp_seq=1 ttl=54 time=12.3 ms
64 bytes from 93.184.216.34: icmp_seq=2 ttl=54 time=11.8 ms
64 bytes from 93.184.216.34: icmp_seq=3 ttl=54 time=12.1 ms
64 bytes from 93.184.216.34: icmp_seq=4 ttl=54 time=12.5 ms

--- www.example.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 11.802/12.175/12.500/0.287 ms
```
> `-c 4` 发 4 个包后停止，`0% packet loss` 和稳定的 RTT 表明网络通畅。

## 大包测试 MTU
```bash
ping -c 4 -s 1472 www.example.com
```
```
PING www.example.com (93.184.216.34) 1472(1500) bytes of data.
1480 bytes from 93.184.216.34: icmp_seq=1 ttl=54 time=12.5 ms
1480 bytes from 93.184.216.34: icmp_seq=2 ttl=54 time=12.3 ms

--- www.example.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss
```
> `-s 1472`（payload 1472 + 28 头 = 1500 总帧），恰好等于标准以太网 MTU 1500，超出则需分片。

## 指定发送间隔
```bash
ping -c 10 -i 0.5 10.0.1.1
```
```
PING 10.0.1.1 (10.0.1.1) 56(84) bytes of data.
64 bytes from 10.0.1.1: icmp_seq=1 ttl=64 time=0.512 ms
64 bytes from 10.0.1.1: icmp_seq=2 ttl=64 time=0.489 ms
...
--- 10.0.1.1 ping statistics ---
10 packets transmitted, 10 received, 0% packet loss, time 4500ms
rtt min/avg/max/mdev = 0.489/0.502/0.550/0.021 ms
```
> `-i 0.5` 每 0.5 秒发一个包，局域网内延迟 < 1ms 且无波动，说明本地网络正常。

## 静默模式（仅看最终统计）
```bash
ping -c 4 -q 8.8.8.8
```
```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.

--- 8.8.8.8 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3003ms
rtt min/avg/max/mdev = 8.201/8.456/8.712/0.189 ms
```
> `-q` 静默模式只输出汇总统计，适合脚本中提取延迟和丢包率数据。
