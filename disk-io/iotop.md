# iotop

## 实时查看有 I/O 活动的进程
```bash
sudo iotop -o
```
```
Total DISK READ:      45.20 M/s | Total DISK WRITE:     120.50 M/s
Current DISK READ:    38.10 M/s | Current DISK WRITE:    105.30 M/s
  TID  PRIO  USER     DISK READ  DISK WRITE  SWAPIN      IO>    COMMAND
 8921 be/4  mysql      12.50 M/s   85.20 M/s  0.00%  78.50%   mysqld
12345 be/4  root        8.30 M/s    0.00 B/s  0.00%  22.10%   python3 backup.py
 5678 be/4  www-data    5.40 M/s   15.60 M/s  0.00%  35.20%   nginx: worker
```
> `-o` 只显示有实际磁盘 I/O 的进程，`IO>` 列数值高的就是当前 I/O 瓶颈来源。

## 批处理模式输出采样
```bash
sudo iotop -bon 3 -d 2
```
```
Total DISK READ:      12.30 M/s | Total DISK WRITE:      45.80 M/s
Current DISK READ:    10.20 M/s | Current DISK WRITE:     42.10 M/s
  TID  PRIO  USER     DISK READ  DISK WRITE  SWAPIN      IO>    COMMAND
 8921 be/4  mysql       5.20 M/s   38.50 M/s  0.00%  65.30%   mysqld
 3456 be/4  root        2.10 M/s    0.00 B/s  0.00%  12.40%   updatedb
```
> `-bon` 组合：批处理模式、只显示有 IO 的进程、不解析主机名，适合输出到日志文件。

## 监控指定进程
```bash
sudo iotop -p 12345
```
```
Total DISK READ:       0.50 M/s | Total DISK WRITE:       8.20 M/s
Current DISK READ:     0.00 B/s | Current DISK WRITE:      7.80 M/s
  TID  PRIO  USER     DISK READ  DISK WRITE  SWAPIN      IO>    COMMAND
12345 be/4  root        0.00 B/s    7.80 M/s  0.00%  18.20%   python3 backup.py
```
> `-p` 只跟踪指定 PID 的 I/O，排除其他进程干扰，精确观察单个进程的磁盘行为。

## 查看累计读写量
```bash
sudo iotop -ao
```
```
Total DISK READ:     12.35 G | Total DISK WRITE:     45.80 G
  TID  PRIO  USER     DISK READ  DISK WRITE  SWAPIN      IO>    COMMAND
 8921 be/4  mysql       8.50 G    35.20 G    0.00%  78.50%   mysqld
12345 be/4  root        2.30 G    45.80 M    0.00%  22.10%   python3 backup.py
```
> `-a` 显示自 `iotop` 启动以来的累计读写量而非瞬时速率，评估进程长期 I/O 开销。
