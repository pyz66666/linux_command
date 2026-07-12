# tcpdump

## 抓取 HTTP 流量并显示内容
```bash
sudo tcpdump -i eth0 -A port 80
```
```
tcpdump: listening on eth0, link-type EN10MB (Ethernet)

10:00:01.234567 IP 10.0.1.100.54321 > 93.184.216.34.80: Flags [P.], seq 1:120, length 119: HTTP: GET / HTTP/1.1
Host: www.example.com
User-Agent: curl/7.81.0

10:00:01.345678 IP 93.184.216.34.80 > 10.0.1.100.54321: Flags [P.], seq 1:500, length 499: HTTP: HTTP/1.1 200 OK
Content-Type: text/html
```
> `-A` 以 ASCII 显示包内容，直接看到 HTTP 请求/响应的明文，调试 Web 应用首选。

## 抓取特定主机的所有流量
```bash
sudo tcpdump -i eth0 -nn host 10.0.1.50
```
```
10:00:01.234567 IP 10.0.1.10.22 > 10.0.1.50.54231: Flags [P.], seq 1000:1500, ack 200, length 500
10:00:01.235012 IP 10.0.1.50.54231 > 10.0.1.10.22: Flags [.], ack 1500, win 65535, length 0
10:00:01.452100 IP 10.0.1.50.61234 > 10.0.1.10.80: Flags [S], seq 987654321, win 65535, length 0
```
> `-nn` 不解析主机名和端口名，直接显示 IP 和端口号，速度更快输出更紧凑。

## 保存到文件供 Wireshark 分析
```bash
sudo tcpdump -i eth0 -w capture.pcap host 10.0.1.50
```
```
tcpdump: listening on eth0, link-type EN10MB (Ethernet), capture size 262144 bytes
^C3458 packets captured
3458 packets received by filter
0 packets dropped by kernel
```
> `-w` 将原始数据包写入 pcap 文件，之后用 Wireshark 可视化分析，比命令行直观得多。

## 抓取 ICMP 包
```bash
sudo tcpdump -i eth0 -nn icmp
```
```
10:00:01.123456 IP 10.0.1.10 > 8.8.8.8: ICMP echo request, id 12345, seq 1, length 64
10:00:01.134567 IP 8.8.8.8 > 10.0.1.10: ICMP echo reply, id 12345, seq 1, length 64
10:00:02.124567 IP 10.0.1.10 > 8.8.8.8: ICMP echo request, id 12345, seq 2, length 64
10:00:02.135678 IP 8.8.8.8 > 10.0.1.10: ICMP echo reply, id 12345, seq 2, length 64
```
> `icmp` 过滤器只抓 ping 请求和回复，验证网络双向可达性，`id` 和 `seq` 匹配请求与回复。

## 排除 SSH 避免干扰自己
```bash
sudo tcpdump -i eth0 -nn not port 22
```
```
10:00:01.234567 IP 10.0.1.100.54321 > 93.184.216.34.443: Flags [S], seq 123456789, win 65535, length 0
10:00:01.250123 IP 10.0.1.10.53 > 8.8.8.8.53: 1234+ A? www.example.com. (33)
```
> `not port 22` 排除 SSH 流量，避免远程管理自己的抓包也被捕获，减少干扰。

## 只抓 TCP SYN 包（连接建立）
```bash
sudo tcpdump -i eth0 -nn 'tcp[tcpflags] & tcp-syn != 0'
```
```
10:00:01.234567 IP 10.0.1.100.54321 > 93.184.216.34.443: Flags [S], seq 123456789, win 65535, length 0
10:00:01.300123 IP 10.0.1.100.54322 > 203.0.113.50.80: Flags [S], seq 987654321, win 65535, length 0
```
> BPF 过滤表达式只捕获 SYN 包，快速统计哪些连接正在发起，排查频繁建连问题。
