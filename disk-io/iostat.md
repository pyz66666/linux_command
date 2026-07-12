# iostat

## 查看磁盘 I/O 扩展统计
```bash
iostat -x 1 2
```
```
Linux 5.15.0 (server01)    07/12/2026      _x86_64_        (8 CPU)

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           2.35    0.00    1.12    5.80    0.00   90.73

Device     r/s     w/s     rkB/s   wkB/s   await  r_await w_await  %util
sda       45.00  120.00   2048.00 4096.00   12.50    8.20   14.10  85.30
sdb        3.00   15.00    128.00 1024.00    5.20    3.50    6.80  12.00
```
> `-x` 显示扩展指标：`await` 是 I/O 平均等待时间（ms），`%util` 是设备繁忙度，接近 100% 说明磁盘饱和。

## 仅查看磁盘统计（不显示 CPU）
```bash
iostat -dm 1 2
```
```
Device     tps    MB_read/s  MB_wrtn/s  MB_read  MB_wrtn
sda      165.00      2.00       4.00       2.00     4.00
sdb       18.00      0.13       1.00       0.13     1.00
```
> `-dm` 只显示设备吞吐数据，以 MB 为单位，适合只看磁盘不看 CPU 的场景。

## 监控指定磁盘
```bash
iostat -x -p sda 1
```
```
Device     r/s     w/s     rkB/s   wkB/s   await  r_await w_await  %util
sda       50.00  130.00   2500.00 5200.00   15.20    9.10   16.80  92.10
sda       48.00  125.00   2400.00 5100.00   14.80    8.90   16.20  90.50
```
> `-p sda` 仅监控 `/dev/sda`，每秒刷新一次，持续观察单盘性能变化。

## 带时间戳持续监控
```bash
iostat -xt 1
```
```
10:00:01 AM   Device     r/s     w/s    await  %util
10:00:01 AM   sda       45.00  120.00   12.50  85.30
10:00:02 AM   sda       52.00  135.00   18.20  94.10
```
> `-t` 每行带时间戳，排查间歇性 I/O 毛刺时能精准定位异常发生的时刻。
