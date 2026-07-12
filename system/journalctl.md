# journalctl

## 查看服务最近日志
```bash
journalctl -u nginx.service -n 20 --no-pager
```
```
7月 12 09:23:15 my-server systemd[1]: Starting nginx - high performance web server...
7月 12 09:23:16 my-server nginx[12345]: nginx: configuration file /etc/nginx/nginx.conf test is successful
7月 12 09:23:16 my-server systemd[1]: Started nginx - high performance web server.
7月 12 09:30:01 my-server nginx[12346]: 192.168.1.100 - - "GET / HTTP/1.1" 200 612 "-" "curl/8.0"
7月 12 10:00:00 my-server nginx[12347]: [error] *42 connect() failed (111: Connection refused) while connecting to upstream
```
> `-u` 按服务过滤，最后一条 connect() failed 表示 nginx 连接上游服务失败（如后端未启动）。

## 按时间范围和级别过滤
```bash
journalctl --since "2026-07-12 09:00:00" --until "2026-07-12 10:00:00" -p err
```
```
7月 12 09:15:23 my-server kernel: iwlwifi 0000:00:14.3: WRT: Invalid buffer destination
7月 12 09:18:45 my-server sshd[8901]: Failed password for root from 192.168.1.200 port 54321 ssh2
7月 12 09:22:10 my-server mysqld[5678]: [ERROR] InnoDB: Unable to lock ./ibdata1 error: 11
```
> `--since/--until` 限定时间范围，`-p err` 只看 error 级别以上，快速定位问题时段。

## 实时跟踪日志
```bash
journalctl -f
```
```
7月 12 10:35:42 my-server sshd[12345]: Accepted publickey for user from 192.168.1.50 port 45678
7月 12 10:35:45 my-server sudo[12346]:     user : TTY=pts/0 ; PWD=/home/user ; USER=root ; COMMAND=/usr/bin/apt update
```
> `-f` 类似 tail -f，实时跟踪新产生的日志，可以看到用户登录和 sudo 操作。

## 查看本次启动的日志
```bash
journalctl -b | tail -5
```
```
7月 12 09:00:01 my-server systemd[1]: Startup finished in 3.456s (kernel) + 8.901s (userspace) = 12.357s.
7月 12 09:00:02 my-server systemd[1]: Reached target Multi-User System.
7月 12 09:00:03 my-server NetworkManager[890]: <info>  device (eth0): carrier: link connected
```
> `-b` 只看本次启动后的日志，`-b -1` 看上上次启动（排查上次为何重启）。

## 查看内核消息
```bash
journalctl -k | tail -5
```
```
7月 12 09:00:01 my-server kernel: EXT4-fs (sda1): mounted filesystem with ordered data mode
7月 12 09:00:01 my-server kernel: e1000e 0000:00:1f.6 eth0: NIC Link is Up 1000 Mbps Full Duplex
```
> `-k` 只显示内核消息，等同于 dmesg 但带 systemd 时间戳和持久化存储。
