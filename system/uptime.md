# uptime

## 快速查看系统状态
```bash
uptime
```
```
 10:35:42 up 45 days,  3:21,  2 users,  load average: 1.23, 2.45, 3.01
```
> 运行 45 天，2 用户登录，负载 1.23/2.45/3.01（8 核系统下负载很低）。

## 只看运行时间
```bash
uptime -p
```
```
up 6 weeks, 3 days, 3 hours, 21 minutes
```
> `-p` 以人类可读格式（pretty）显示运行时长：6 周 3 天 3 小时 21 分钟。

## 查看系统启动时间
```bash
uptime -s
```
```
2026-05-28 07:14:21
```
> 系统于 2026 年 5 月 28 日 07:14 启动，距现已运行约一个半月。

## 判断负载趋势
```bash
uptime; uptime
```
```
 10:35:42 up 45 days,  3:21,  2 users,  load average: 4.50, 3.20, 2.10
```
> 1min 负载 > 5min > 15min（4.50 > 3.20 > 2.10）说明负载正在快速上升。

## 判断 CPU 是否过载
```bash
nproc && uptime
```
```
8
 10:35:42 up 45 days,  3:21,  2 users,  load average: 9.50, 8.30, 7.20
```
> 8 核系统但负载 9.50 > 8，说明有进程在排队等待 CPU，系统处于过载状态。
