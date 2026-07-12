# iperf

## TCP 带宽测试
```bash
iperf3 -c 10.0.1.50 -t 10
```
```
Connecting to host 10.0.1.50, port 5201
[  5] local 10.0.1.10 port 54321 connected to 10.0.1.50 port 5201
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec   113 MBytes   948 Mbits/sec    0   1.12 MBytes
[  5]   1.00-2.00   sec   112 MBytes   941 Mbits/sec    0   1.25 MBytes
...
[  5]   0.00-10.00  sec  1.09 GBytes   941 Mbits/sec    0             sender
[  5]   0.00-10.04  sec  1.09 GBytes   934 Mbits/sec                  receiver

iperf Done.
```
> `Retr=0` 零重传说明网络质量极好，941 Mbps 接近千兆线速，`Cwnd` 逐步增长表明 TCP 慢启动正常。

## 多并行流测试
```bash
iperf3 -c 10.0.1.50 -P 10
```
```
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec   112 MBytes  94.2 Mbits/sec    0             sender
[  7]   0.00-10.00  sec   111 MBytes  93.1 Mbits/sec    2             sender
[  9]   0.00-10.00  sec   113 MBytes  94.8 Mbits/sec    0             sender
...
[SUM]   0.00-10.00  sec  1.09 GBytes  940 Mbits/sec    5             sender
```
> `-P 10` 同时 10 个 TCP 流，`[SUM]` 是总带宽，个别流有少量重传但不影响整体吞吐。

## UDP 带宽和丢包测试
```bash
iperf3 -c 10.0.1.50 -u -b 100M -t 5
```
```
Connecting to host 10.0.1.50, port 5201
[ ID] Interval           Transfer     Bitrate         Jitter    Lost/Total Datagrams
[  5]   0.00-5.00  sec  59.6 MBytes   100 Mbits/sec  0.052 ms  0/42651 (0%)
[  5]   0.00-5.00  sec  59.6 MBytes   100 Mbits/sec  0.052 ms  0/42651 (0%)  receiver

iperf Done.
```
> `-u -b 100M` UDP 模式以 100Mbps 速率发送，`Jitter=0.052ms` 极低抖动，`Lost=0%` 无丢包。

## 反向测试（测下载带宽）
```bash
iperf3 -c 10.0.1.50 -R
```
```
Connecting to host 10.0.1.50, port 5201
Reverse mode, remote host 10.0.1.50 is sending
[ ID] Interval           Transfer     Bitrate
[  5]   0.00-10.00  sec  1.12 GBytes   960 Mbits/sec                  receiver

iperf Done.
```
> `-R` 反向模式：服务端发送、客户端接收，测的是下载带宽而非上传，适合排查带宽不对称问题。
