# head / tail

## 查看文件前 10 行（默认）
```bash
head app.log
```
```
2025-07-12 08:00:00 INFO Server starting
2025-07-12 08:00:01 INFO Loading config
2025-07-12 08:00:02 INFO Connecting to database
...
2025-07-12 08:00:09 INFO Ready
```
> 默认显示文件前 10 行，适合快速查看文件开头。

## 查看文件最后 10 行（默认）
```bash
tail app.log
```
```
2025-07-12 10:29:55 DEBUG Processing request #998
2025-07-12 10:29:57 DEBUG Request #998 completed
2025-07-12 10:30:00 INFO Health check OK
...
```
> 默认显示文件最后 10 行，适合查看最新日志。

## 指定行数
```bash
head -n 5 data.csv
```
```
id,name,department,salary
1,张三,研发部,15000
2,李四,运维部,12000
3,王五,测试部,10000
4,赵六,研发部,18000
```
> `-n 5` 显示前 5 行，包括 CSV 表头。

## 实时跟踪日志
```bash
tail -f /var/log/nginx/access.log
```
```
192.168.1.100 - - [12/Jul/2025:10:30:01] "GET /index.html" 200 2048
192.168.1.101 - - [12/Jul/2025:10:30:02] "POST /api/login" 200 512
192.168.1.102 - - [12/Jul/2025:10:30:03] "GET /style.css" 200 1024
```
> `-f` 持续监控文件新增内容，Ctrl+C 退出，新日志实时显示。

## 跳过前 N-1 行，从第 N 行开始
```bash
tail -n +100 large.log | head -5
```
```
2025-07-12 08:05:00 DEBUG Row 100
2025-07-12 08:05:01 INFO Row 101
2025-07-12 08:05:02 WARN Row 102
2025-07-12 08:05:03 ERROR Row 103
2025-07-12 08:05:04 INFO Row 104
```
> `tail -n +100` 从第 100 行输出到末尾，管道给 `head` 取其中 5 行。

## 多文件时显示文件名头
```bash
tail -n 2 access.log error.log
```
```
==> access.log <==
192.168.1.105 - - [12/Jul/2025:10:30:10] "GET /favicon.ico" 200 512
192.168.1.106 - - [12/Jul/2025:10:30:11] "GET /about.html" 200 4096

==> error.log <==
2025/07/12 10:28:00 timeout connecting to backend
2025/07/12 10:29:50 upstream server 10.0.0.5:8080 is down
```
> 多文件时自动添加 `==> 文件名 <==` 标题，便于区分来源。
