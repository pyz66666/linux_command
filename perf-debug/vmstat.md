# vmstat

## 每秒输出系统概况
```bash
vmstat 1 5
```
```
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 1  0      0 3876544 345612 2456789    0    0    12    45  345 1234  3  1 95  1  0
 2  0      0 3870123 345620 2457890    0    0     0   128 1234 3456 12  4 80  4  0
 1  0      0 3865432 345620 2460123    0    0     0     0  567 2345  5  2 93  0  0
 0  1      0 3862000 345620 2461234    0    0     0  4096  234 1234  2  1 87 10  0
 1  0      0 3871000 345624 2459999    0    0     0    56  456 2345  4  2 94  0  0
```
> 第 1 行是启动至今平均值，从第 2 行开始才是实时数据；r=运行队列，b=I/O 等待，si/so=swap 进出，wa=I/O 等待。

## 查看内存统计汇总
```bash
vmstat -s
```
```
      8167732 K total memory
      3876456 K used memory
       429736 K free memory
       345612 K buffer memory
      2456789 K swap cache
      2097148 K total swap
            0 K used swap
```
> `-s` 一次性输出内存总量、使用量、swap 等汇总数据，used swap=0 表示无内存压力。

## 显示活跃/非活跃内存
```bash
vmstat -a 1 3
```
```
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free  inact active   si   so    bi    bo   in   cs us sy id wa st
 1  0      0 412345 1234567 2345678    0    0    12    45  345 1234  3  1 95  1  0
```
> `-a` 显示 active（正在使用）和 inact（最近未用但可回收）内存，判断缓存回收潜力。

## 显示磁盘 I/O 统计
```bash
vmstat -d
```
```
disk- ------------reads------------ ------------writes----------- -----IO------
       total merged sectors      ms  total merged sectors      ms    cur    sec
sda    12345   3456 2345678   45678  56789  12345 45678901 1234567      0    234
nvme0n1 345678 12345 45678901  34567 234567  67890 34567890  987654      0    123
```
> `-d` 显示每块磁盘的读写次数、扇区数和耗时，对比不同磁盘的 I/O 负载。

## 带时间戳的宽输出
```bash
vmstat -wt 2 3
```
```
  procs -----------------------memory---------------------- ---swap-- -----io---- -system-- --------cpu-------- -----timestamp-----
   r  b         swpd         free         buff        cache   si   so    bi    bo   in   cs  us  sy  id  wa  st                 CST
   1  0            0      3876544       345612      2456789    0    0    12    45  345 1234   3   1  95   1   0 2026-07-12 10:35:42
```
> `-w` 宽输出避免字段截断，`-t` 添加时间戳，适合持续监控并留存记录。
