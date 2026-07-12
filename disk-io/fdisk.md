# fdisk

## 查看所有磁盘分区（fdisk）
```bash
sudo fdisk -l
```
```
Disk /dev/sda: 50 GiB, 53687091200 bytes, 104857600 sectors
Disk model: VBOX HARDDISK
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes

Device     Boot   Start       End   Sectors  Size Id Type
/dev/sda1  *       2048 104855551 104853504   50G 83 Linux

Disk /dev/sdb: 200 GiB, 214748364800 bytes, 419430400 sectors
Device     Boot   Start       End   Sectors  Size Id Type
/dev/sdb1          2048 314574847 314572800  150G 83 Linux
/dev/sdb2     314574848 419430399 104855552   50G 83 Linux
```
> `-l` 列出系统所有磁盘的分区表，包括大小、扇区、分区类型（`83`=Linux，`82`=swap）。

## 查看磁盘分区详情（parted）
```bash
sudo parted -l
```
```
Model: ATA VBOX HARDDISK (scsi)
Disk /dev/sda: 53.7GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos

Number  Start   End     Size    Type     File system  Flags
 1      1049kB  53.7GB  53.7GB  primary  ext4         boot

Model: ATA VBOX HARDDISK (scsi)
Disk /dev/sdb: 215GB
Partition Table: gpt

Number  Start   End     Size    File system  Name     Flags
 1      1049kB  161GB   161GB   ext4         primary
 2      161GB   215GB   53.7GB  ext4         backup
```
> `parted -l` 比 fdisk 更清晰，显示分区表类型（msdos=MBR，gpt=GPT）和文件系统。

## 查看指定磁盘的分区表
```bash
sudo fdisk -l /dev/sda
```
```
Disk /dev/sda: 50 GiB, 53687091200 bytes, 104857600 sectors
Disk model: VBOX HARDDISK
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes

Device     Boot   Start       End   Sectors  Size Id Type
/dev/sda1  *       2048 104855551 104853504   50G 83 Linux
```
> `*` 在 Boot 列表示该分区可引导，`Start/End` 是扇区起止位置。

## 脚本化创建 GPT 分区
```bash
sudo parted -s /dev/sdb mklabel gpt
sudo parted -s /dev/sdb mkpart primary ext4 0% 100%
```
```
$ sudo parted /dev/sdb print
Model: ATA VBOX HARDDISK (scsi)
Disk /dev/sdb: 215GB
Partition Table: gpt

Number  Start   End     Size    File system  Name     Flags
 1      1049kB  215GB   215GB                primary
```
> `parted -s` 非交互脚本模式：先创建 GPT 标签，再创建一个占满全盘的主分区。
