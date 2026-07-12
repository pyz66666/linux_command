# iozone

## 基本顺序读写测试
```bash
iozone -s 128m -r 4k -r 64k -r 1m -i 0 -i 1
```
```
        Iozone: Performance Test of File I/O

        Record Size  4 KB
        File size set to 131072 KB

                                                          random  random
              KB  reclen   write rewrite    read  reread    read   write
          131072       4  185234  192450  210340  212150
          131072      64  342100  348200  389500  391200
          131072    1024  410200  415340  450100  451200

iozone test complete.
```
> 三组块大小（4K/64K/1M）的读写对比：块越大吞吐越高，1M 块顺序写 410MB/s 而 4K 仅 185MB/s。

## 自动模式输出 Excel 报告
```bash
iozone -Rab result.xls -g 512m
```
```
        Iozone: Performance Test of File I/O
        Auto Mode: testing with file sizes from 64K to 512M

        Output is in Kbytes/sec
        Excel output is in file: result.xls

iozone test complete.
```
> `-Ra` 自动测试多种文件大小和块大小组合，`-b` 生成 Excel 报告用于绘制性能曲线图。

## 多线程并发读写测试
```bash
iozone -t 4 -s 256m -r 1m -i 0 -i 1
```
```
        Iozone: Performance Test of File I/O
        Running 4 threads with file size 262144 KB

        Children see throughput for  4 initial writers = 1203400.00 KB/sec
        Children see throughput for  4 rewriters       = 1185600.00 KB/sec
        Children see throughput for  4 readers         = 1560800.00 KB/sec
        Children see throughput for  4 re-readers      = 1572100.00 KB/sec

iozone test complete.
```
> `-t 4` 四个线程并发测试，评估文件系统在多进程并发 I/O 下的总吞吐量。
