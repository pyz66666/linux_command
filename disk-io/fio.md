# fio

## 测试随机读 IOPS（模拟数据库场景）
```bash
fio --name=randread --rw=randread --bs=4k --size=1G --iodepth=32 --numjobs=4 \
    --runtime=60 --direct=1 --group_reporting
```
```
randread: (groupid=0, jobs=4): err= 0: pid=12345
  read: IOPS=125k, BW=489MiB/s (513MB/s)(28.6GiB/60001msec)
    slat (usec): min=2, max=150, avg= 4.20, stdev= 1.50
    clat (usec): min=10, max=5000, avg=245.30, stdev=85.40
     lat (usec): min=15, max=5010, avg=249.50, stdev=86.10
```
> 4K 随机读，`IOPS=125k` 是核心指标，`clat` 平均 245μs 是用户感知的单次 I/O 延迟。

## 测试顺序写带宽
```bash
fio --name=seqwrite --rw=write --bs=1m --size=4G --iodepth=16 --numjobs=1 \
    --runtime=60 --direct=1 --group_reporting
```
```
seqwrite: (groupid=0, jobs=1): err= 0: pid=12346
  write: IOPS=502, BW=502MiB/s (527MB/s)(29.4GiB/60001msec)
    clat (msec): min=15, max=85, avg=31.50, stdev=8.20
```
> 1M 块顺序写，`BW=502MiB/s` 是磁盘的顺序写带宽上限，适合评估大文件传输能力。

## 混合读写测试（70% 读 30% 写）
```bash
fio --name=mixed --rw=randrw --rwmixread=70 --bs=4k --size=1G \
    --iodepth=32 --numjobs=4 --runtime=60 --direct=1 --group_reporting
```
```
mixed: (groupid=0, jobs=4): err= 0: pid=12347
  read: IOPS=87.5k, BW=342MiB/s (358MB/s)(20.0GiB/60001msec)
  write: IOPS=37.5k, BW=147MiB/s (154MB/s)(8610MiB/60001msec)
```
> `--rwmixread=70` 设定 70% 读 30% 写，模拟真实应用中读写混合的负载模式。
