# du

## 查看当前目录各子目录大小
```bash
du -h -d 1
```
```
4.0K    ./Desktop
12K     ./Documents
1.2G    ./Downloads
328M    ./projects
1.5G    .
```
> `-d 1` 只展开一层子目录，快速定位哪个文件夹占用最多空间。

## 查看某个目录的总大小
```bash
du -sh /var/log
```
```
1.2G    /var/log
```
> `-s` 仅输出汇总大小，`-h` 人类可读，是最常用的快速估大小组合。

## 找出当前目录下最大的几个文件
```bash
du -ah | sort -rh | head -5
```
```
512M    ./backup/database.dump
256M    ./logs/app.log
128M    ./data/cache.dat
64M     ./vendor/lib/biglib.so
32M     ./photos/raw/img_001.raw
```
> `-a` 同时显示文件（默认只显示目录），配合 `sort -rh` 降序排列，`head` 取前 N 个。

## 按大小排序查看子目录
```bash
du -h -d 1 | sort -rh
```
```
1.5G    .
1.2G    ./Downloads
328M    ./projects
12K     ./Documents
4.0K    ./Desktop
```
> 将 `du` 输出通过管道交给 `sort -rh`，最大的目录排在最前，一眼识别磁盘大户。

## 排除指定目录后统计
```bash
du -sh --exclude=.git .
```
```
328M    .
```
> `--exclude=.git` 忽略 Git 仓库目录，避免版本控制文件干扰空间估算。
