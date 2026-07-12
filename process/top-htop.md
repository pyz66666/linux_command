# top / htop

## 启动实时监控
```bash
top
```
```
top - 10:30:15 up 15 days,  2:15,  3 users,  load average: 0.52, 0.38, 0.29
Tasks: 187 total,   2 running, 185 sleeping,   0 stopped,   0 zombie
%Cpu(s):  12.5 us,   3.2 sy,   0.0 ni,  84.0 id,   0.0 wa,   0.3 hi,   0.0 si
MiB Mem :  15786 total,   2341 free,   8450 used,   4995 buff/cache
MiB Swap:   2048 total,   1800 free,    248 used.   6500 avail Mem

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
12345 alice     20   0  812340 215400  12500 S   4.3   2.1   0:15.32 python
  987 mysql     20   0 1523400 420000  18000 S   2.1   4.0  12:05.10 mysqld
```
> 头部显示系统负载、CPU、内存概况，进程列表每 3 秒自动刷新，按 `q` 退出。

## 指定刷新间隔
```bash
top -d 1
```
```
top - 10:30:15 up 15 days,  2:15,  3 users,  load average: 0.52, 0.38, 0.29
...
```
> `-d 1` 每 1 秒刷新一次，更快看到变化。

## 只监控指定用户
```bash
top -u www-data
```
```
  PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
 1456 www-data  20   0   85640  12400   3200 S   0.0   0.1   0:10.12 nginx
 1457 www-data  20   0   85640  12400   3200 S   0.0   0.1   0:12.25 nginx
```
> `-u` 只显示 `www-data` 用户的进程。

## 批处理模式（输出到文件）
```bash
top -b -n 1 > system_status.txt
```
```
```
> `-b` 批处理模式、`-n 1` 只运行一次后退出，适合 cron 定时采集。

## 启动 htop（增强版）
```bash
htop
```
```
  1  [|||||||||||||||                25.0%]   Tasks: 45, 88 thr; 2 running
  2  [||||||||||                     18.7%]   Load average: 0.52 0.38 0.29
  Mem[|||||||||||||||||||||||||||||  8450/15786MB]   Uptime: 15 days
  Swp[||                              248/2048MB]

  PID USER      PRI  NI  VIRT   RES   SHR S CPU% MEM%   TIME+  Command
 1234 alice      20   0  812M  215M 12500 S  4.3  2.1  0:15.32 python app.py
  987 mysql      20   0 1.45G  420M 18000 S  2.1  4.0 12:05.10 /usr/sbin/mysqld
```
> `htop` 彩色显示、CPU 条形图、支持鼠标点击和 F 键交互，需单独安装。
