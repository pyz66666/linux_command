# nmap

## 扫描常用 1000 端口
```bash
nmap 10.0.1.50
```
```
Starting Nmap 7.94 ( https://nmap.org ) at 2026-07-12 10:00 CST
Nmap scan report for 10.0.1.50
Host is up (0.0012s latency).
Not shown: 995 closed tcp ports (reset)
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
443/tcp  open  https
3306/tcp open  mysql
8080/tcp open  http-proxy

Nmap done: 1 IP address (1 host up) scanned in 2.45 seconds
```
> 默认扫描 top 1000 端口，5 个端口开放，995 个关闭，`0.0012s` 延迟说明同网段内。

## 扫描指定端口
```bash
nmap -p 22,80,443,3306 10.0.1.50
```
```
Nmap scan report for 10.0.1.50
Host is up (0.0010s latency).

PORT     STATE  SERVICE
22/tcp   open   ssh
80/tcp   open   http
443/tcp  open   https
3306/tcp closed mysql

Nmap done: 1 IP address (1 host up) scanned in 0.50 seconds
```
> `-p` 指定端口列表，比全 1000 端口快得多，目标明确时推荐使用。

## 服务版本检测
```bash
sudo nmap -sV 10.0.1.50
```
```
Nmap scan report for 10.0.1.50
Host is up (0.0012s latency).
Not shown: 995 closed tcp ports (reset)
PORT     STATE SERVICE  VERSION
22/tcp   open  ssh      OpenSSH 8.9p1 Ubuntu 3ubuntu0.7
80/tcp   open  http     nginx 1.24.0
443/tcp  open  ssl/http nginx 1.24.0
3306/tcp open  mysql    MySQL 8.0.35
8080/tcp open  http     Apache Tomcat 9.0.80

Service detection performed.
Nmap done: 1 IP address (1 host up) scanned in 12.34 seconds
```
> `-sV` 探测服务精确版本号，如 `nginx 1.24.0`、`MySQL 8.0.35`，用于安全审计和漏洞评估。

## 扫描子网存活主机
```bash
nmap -sn 10.0.1.0/24
```
```
Nmap scan report for 10.0.1.1
Host is up (0.00089s latency).
Nmap scan report for 10.0.1.10
Host is up (0.0012s latency).
Nmap scan report for 10.0.1.50
Host is up (0.0015s latency).
Nmap done: 256 IP addresses (3 hosts up) scanned in 3.01 seconds
```
> `-sn`（Ping Scan）只做主机发现不扫端口，3 秒内扫描整个 /24 子网的 256 个地址。

## 全端口扫描
```bash
nmap -p- 10.0.1.50
```
```
Nmap scan report for 10.0.1.50
Host is up (0.0010s latency).
Not shown: 65529 closed tcp ports (reset)
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
443/tcp  open  https
3306/tcp open  mysql
8080/tcp open  http-proxy
9090/tcp open  zeus-admin

Nmap done: 1 IP address (1 host up) scanned in 45.23 seconds
```
> `-p-` 扫描全部 65535 个端口，发现一个非标准端口 9090，默认 1000 端口扫描无法发现。
