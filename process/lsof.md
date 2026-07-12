# lsof

## 查看哪个进程占用了端口
```bash
lsof -i :80
```
```
COMMAND   PID  USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
nginx    1234  root    6u  IPv4  25123      0t0  TCP *:http (LISTEN)
nginx    1235  www     6u  IPv4  25123      0t0  TCP *:http (LISTEN)
```
> nginx 的 master（root）和 worker（www-data）进程正在监听 80 端口。

## 查看进程打开了哪些文件
```bash
lsof -p 1234
```
```
COMMAND  PID USER   FD   TYPE DEVICE SIZE/OFF   NODE NAME
nginx   1234 root  cwd    DIR  259,2     4096  50001 /etc/nginx
nginx   1234 root  rtd    DIR  259,2     4096      2 /
nginx   1234 root  txt    REG  259,2  1048560 120000 /usr/sbin/nginx
nginx   1234 root  mem    REG  259,2  2150400 110000 /usr/lib/x86_64-linux-gnu/libc.so.6
nginx   1234 root    0r   CHR    1,3      0t0   1029 /dev/null
nginx   1234 root    6u  IPv4    25123      0t0    TCP *:http (LISTEN)
```
> `FD` 为文件描述符（`txt`=程序代码，`mem`=内存映射库，`6u`=socket），显示进程所有打开的资源。

## 查看用户打开的所有文件
```bash
lsof -u alice | head -5
```
```
COMMAND  PID  USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
bash    1206 alice  cwd    DIR  259,2     4096 50000 /home/alice
bash    1206 alice  rtd    DIR  259,2     4096     2 /
bash    1206 alice  txt    REG  259,2  1183448 90000 /usr/bin/bash
bash    1206 alice  mem    REG  259,2  2150400 110000 /usr/lib/x86_64-linux-gnu/libc.so.6
```
> `-u` 列出指定用户打开的所有文件、socket 和设备。

## 查看所有网络连接
```bash
lsof -i TCP | head -5
```
```
COMMAND  PID  USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
sshd     620  root    3u  IPv4  20000      0t0  TCP *:ssh (LISTEN)
sshd    1200  root    4u  IPv4  23500      0t0  TCP server:ssh->client:54321 (ESTABLISHED)
nginx   1234  root    6u  IPv4  25123      0t0  TCP *:http (LISTEN)
python 12345 alice    3u  IPv4  28888      0t0  TCP localhost:8080 (LISTEN)
```
> `-i TCP` 只显示 TCP 连接，`LISTEN` 表示监听中，`ESTABLISHED` 表示已建立连接。

## 查看目录下被打开的文件
```bash
lsof +D /var/log
```
```
COMMAND  PID  USER   FD   TYPE DEVICE SIZE/OFF   NODE NAME
nginx   1235  www    5w   REG  259,2   245760 150000 /var/log/nginx/access.log
nginx   1235  www    6w   REG  259,2    12345 150001 /var/log/nginx/error.log
syslogd  450  root   3w   REG  259,2  1048576 145000 /var/log/syslog
```
> `+D` 递归列出指定目录下所有被进程打开的文件。
