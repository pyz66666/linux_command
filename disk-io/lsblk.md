# lsblk

## 查看所有块设备
```bash
lsblk
```
```
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda      8:0    0    50G  0 disk
├─sda1   8:1    0    50G  0 part /
sdb      8:16   0   200G  0 disk
├─sdb1   8:17   0   150G  0 part /data
└─sdb2   8:18   0    50G  0 part /backup
sr0     11:0    1  1024M  0 rom
```
> 树形结构展示磁盘（disk）和分区（part）的层级关系，以及每个分区的挂载点。

## 查看设备及文件系统详细信息
```bash
lsblk -f
```
```
NAME   FSTYPE LABEL  UUID                                 MOUNTPOINT
sda
└─sda1 ext4   root   a1b2c3d4-xxxx-yyyy-zzzz-123456789abc /
sdb
├─sdb1 ext4   data   8f3a2b1c-xxxx-yyyy-zzzz-987654321def /data
└─sdb2 ext4   backup f1e2d3c4-xxxx-yyyy-zzzz-abcdef123456 /backup
```
> `-f` 显示文件系统类型、卷标和 UUID，写 `/etc/fstab` 时推荐用 UUID 而非设备名。

## 查看指定磁盘
```bash
lsblk /dev/sdb
```
```
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sdb      8:16   0   200G  0 disk
├─sdb1   8:17   0   150G  0 part /data
└─sdb2   8:18   0    50G  0 part /backup
```
> 只查看某一块磁盘的分区结构，避免其他设备干扰。

## 自定义输出列
```bash
lsblk -o NAME,SIZE,TYPE,MOUNTPOINT
```
```
NAME     SIZE TYPE MOUNTPOINT
sda       50G disk
└─sda1    50G part /
sdb      200G disk
├─sdb1   150G part /data
└─sdb2    50G part /backup
```
> `-o` 按需选择输出列，脚本处理时只取必要字段，输出更精简。
