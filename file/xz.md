# xz

## 压缩文件
```bash
xz largefile.log
```
```
```
> 原文件被替换为 `largefile.log.xz`，压缩率通常比 gzip 高 30%。

## 压缩并显示详情
```bash
xz -v data.csv
```
```
data.csv (1/1)
  100 %     12.3 MiB / 45.0 MiB = 0.273
```
> 压缩后 12.3MB，原始 45.0MB，压缩比 27.3%，体积缩小了约 73%。

## 多线程加速压缩
```bash
xz -T0 -v largefile.log
```
```
largefile.log (1/1)
  100 %     18.5 MiB / 60.0 MiB = 0.308   4.5 MiB/s   0:13
```
> `-T0` 使用所有 CPU 核心并行压缩，大幅缩短时间。

## 解压文件
```bash
xz -d largefile.log.xz
```
```
```
> `-d` 解压模式，恢复原始文件并删除 `.xz` 文件。

## 解压并保留原文件
```bash
xz -dk file.xz
```
```
```
> `-k` 保留原始的 `.xz` 文件，同时生成解压后的文件。

## 测试压缩文件完整性
```bash
xz -t archive.xz
```
```
```
> `-t` 无输出表示文件完整，有错误会报告损坏。

## 低压缩级别快速压缩
```bash
xz -1k app.log
```
```
```
> `-1` 最快压缩级别，适合临时压缩，`-k` 保留原始文件。
