# df

## 查看所有文件系统的磁盘空间使用
```bash
df -h
```
```
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G   32G   16G  67% /
/dev/sdb1       200G  145G   55G  73% /data
tmpfs           3.9G  2.1M  3.9G   1% /dev/shm
```
> `-h` 以人类可读格式显示，一眼看出各分区的总容量、已用、可用和使用率。

## 同时显示文件系统类型
```bash
df -hT
```
```
Filesystem     Type      Size  Used Avail Use% Mounted on
/dev/sda1      ext4       50G   32G   16G  67% /
/dev/sdb1      xfs       200G  145G   55G  73% /data
tmpfs          tmpfs     3.9G  2.1M  3.9G   1% /dev/shm
```
> `-T` 额外显示文件系统类型（ext4/xfs/tmpfs），排查问题时一眼看清分区格式。

## 检查 inode 使用情况
```bash
df -i
```
```
Filesystem      Inodes  IUsed   IFree IUse% Mounted on
/dev/sda1      3276800 450123 2826677   14% /
/dev/sdb1     13107200 980000 12127200    8% /data
```
> 小文件过多时即使磁盘空间未满，inode 耗尽也无法创建新文件，`-i` 专门排查此类问题。

## 仅查看指定类型的文件系统
```bash
df -h -t ext4
```
```
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G   32G   16G  67% /
```
> `-t ext4` 过滤仅显示 ext4 分区，`-x tmpfs` 则可排除伪文件系统。

## 快速查看当前目录所在分区的空间
```bash
df -h .
```
```
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G   32G   16G  67% /
```
> `.` 代表当前目录，无需记住挂载路径也能立即知道还剩多少空间。

## 显示所有分区的总计行
```bash
df -h --total
```
```
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G   32G   16G  67% /
/dev/sdb1       200G  145G   55G  73% /data
tmpfs           3.9G  2.1M  3.9G   1% /dev/shm
total           254G  177G   75G  70% -
```
> `--total` 在末尾追加一行合计，快速掌握整机存储使用全局。
