# ps

## 查看所有进程（BSD 风格）
```bash
ps aux | head -5
```
```
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.1 169740 12340 ?        Ss   Jul10   0:05 /sbin/init
root       523  0.0  0.3 285432 31200 ?        Ssl  Jul10   0:12 /usr/lib/systemd/systemd-journald
alice    12345  0.5  2.1 812340 215400 pts/0  S+   10:30   0:03 python app.py
alice    12350  0.0  0.0  10820  3400 pts/1   R+   10:31   0:00 ps aux
```
> `a` 所有用户、`u` 用户格式、`x` 含无终端进程，`%CPU` `%MEM` 为资源占用百分比。

## 查看所有进程（Unix 风格）
```bash
ps -ef | head -5
```
```
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 Jul10 ?        00:00:05 /sbin/init
root       523     1  0 Jul10 ?        00:00:12 /usr/lib/systemd/systemd-journald
alice    12345  1200  0 10:30 pts/0    00:00:03 python app.py
alice    12350 12345  0 10:31 pts/1    00:00:00 ps -ef
```
> `-e` 所有进程、`-f` 完整格式，含 `PPID`（父进程 ID）。

## 树状显示进程关系
```bash
ps -ef --forest | head -10
```
```
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 Jul10 ?        00:00:05 /sbin/init
root       523     1  0 Jul10 ?        00:00:12  \_ /usr/lib/systemd/systemd-journald
root       620     1  0 Jul10 ?        00:00:30  \_ /usr/sbin/sshd -D
root      1200   620  0 09:00 ?        00:00:02      \_ sshd: alice [priv]
alice     1205  1200  0 09:00 ?        00:00:01          \_ sshd: alice@pts/0
alice     1206  1205  0 09:00 pts/0    00:00:00              \_ -bash
```
> `--forest` 用 `\_` 缩进展示父子层级，清晰看到 sshd 派生链。

## 按内存使用排序
```bash
ps aux --sort=-%mem | head -5
```
```
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
mysql      987  2.1  8.5 1523400 885000 ?      Ssl  Jul10  12:05 mysqld
alice    12345  0.5  2.1 812340 215400 pts/0  S+   10:30   0:03 python app.py
root       523  0.0  0.3 285432 31200 ?        Ssl  Jul10   0:12 systemd-journald
```
> `--sort=-%mem` 按内存占用降序，内存大户排最前。

## 按用户过滤
```bash
ps -u www-data
```
```
  PID TTY          TIME CMD
 1456 ?        00:00:10 nginx
 1457 ?        00:00:12 nginx
 1458 ?        00:00:08 nginx
```
> `-u` 只显示指定用户运行的进程。

## 自定义输出列
```bash
ps -eo pid,ppid,ni,%mem,comm --sort=-ni | head -5
```
```
  PID  PPID  NI %MEM COMMAND
 5432  1234  19  0.0 backup.sh
 6789  1200  10  0.1 tar
 1234  1200   0  2.1 python
```
> `-o` 自定义列，`pid,ppid,ni,%mem,comm` 分别显示 PID、父 PID、nice 值、内存百分比、命令名。
