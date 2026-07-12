# nc

## 测试远程端口是否开放
```bash
nc -zv 10.0.1.50 80
```
```
Connection to 10.0.1.50 80 port [tcp/http] succeeded!
```
> `-z` 仅扫描不发送数据，`-v` 显示结果，快速判断端口是否在监听。

## 扫描端口范围
```bash
nc -zv 10.0.1.50 20-25
```
```
Connection to 10.0.1.50 22 port [tcp/ssh] succeeded!
nc: connect to 10.0.1.50 port 20 (tcp) failed: Connection refused
nc: connect to 10.0.1.50 port 21 (tcp) failed: Connection refused
Connection to 10.0.1.50 25 port [tcp/smtp] succeeded!
```
> 扫描 20-25 端口范围，`succeeded`=开放，`Connection refused`=可达但端口未监听。

## 启动简易 TCP 服务器
```bash
nc -l 8080
```
> `-l` 监听模式，终端会阻塞等待入站连接，连接建立后可在终端中直接收发数据。

## 传输文件（接收端+发送端）
```bash
# 接收端
nc -l 9999 > received_file.tar.gz
# 发送端
nc 10.0.1.20 9999 < file_to_send.tar.gz
```
> 无输出即传输中。接收端先启动监听，发送端连接后传输即开始，Ctrl+C 结束后文件即完整。

## 发送原始 HTTP 请求
```bash
echo -e "GET / HTTP/1.0\r\nHost: example.com\r\n\r\n" | nc example.com 80
```
```
HTTP/1.0 200 OK
Content-Type: text/html; charset=UTF-8
Server: nginx/1.24.0

<!DOCTYPE html>
<html>
...
```
> `nc` 直接与 TCP 服务"对话"，手工构造 HTTP 请求，看到服务器的最原始响应。

## 测试 UDP 端口
```bash
nc -zuv 10.0.1.50 53
```
```
Connection to 10.0.1.50 53 port [udp/domain] succeeded!
```
> `-u` 切换到 UDP 模式，测试 DNS（53）等 UDP 服务是否可达。
