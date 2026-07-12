# free

## 查看内存概况
```bash
free -h
```
```
               total        used        free      shared  buff/cache   available
Mem:           7.7Gi       2.3Gi       412Mi       234Mi       5.0Gi       5.1Gi
Swap:          2.0Gi          0B       2.0Gi
```
> `available` 5.1GB 是应用实际可用内存的关键指标；Swap used=0 表示无内存压力。

## 每秒刷新监控内存
```bash
free -h -s 1
```
```
               total        used        free      shared  buff/cache   available
Mem:           7.7Gi       2.3Gi       412Mi       234Mi       5.0Gi       5.1Gi

Mem:           7.7Gi       2.5Gi       212Mi       234Mi       5.0Gi       4.9Gi

Mem:           7.7Gi       2.8Gi        98Mi       234Mi       4.8Gi       4.5Gi
```
> `-s 1` 每秒刷新，used 持续增长且 available 持续下降，可能是内存泄漏信号。

## 以 MB 为单位显示
```bash
free -m
```
```
               total        used        free      shared  buff/cache   available
Mem:            7884        2355         412         234        5120        5222
Swap:           2047           0        2047
```
> `-m` 以 MB 为单位，适合脚本解析和精确数值比较。

## 显示合计行
```bash
free -h -t
```
```
               total        used        free      shared  buff/cache   available
Mem:           7.7Gi       2.3Gi       412Mi       234Mi       5.0Gi       5.1Gi
Swap:          2.0Gi          0B       2.0Gi
Total:         9.7Gi       2.3Gi       2.4Gi
```
> `-t` 在底部显示物理内存 + swap 的合计，Total available=2.4Gi 是 free swap + Mem available。

## 宽模式分开 buff 和 cache
```bash
free -hw
```
```
               total        used        free     buffers       cache   available
Mem:           7.7Gi       2.3Gi       412Mi       338Mi       4.7Gi       5.1Gi
Swap:          2.0Gi          0B       2.0Gi
```
> `-w` 将 buff/cache 拆分为 buffers（块设备元数据）和 cache（页缓存），精细分析缓存构成。
