# mount

## 查看当前所有挂载
```bash
mount | column -t
```
```
/dev/sda1       on  /          type  ext4    (rw,relatime)
/dev/sdb1       on  /data      type  ext4    (rw,nosuid,noexec)
tmpfs           on  /dev/shm   type  tmpfs   (rw,nosuid,nodev)
/dev/sr0        on  /mnt/iso   type  iso9660 (ro,relatime)
```
> `column -t` 对齐列输出，一目了然地看到设备、挂载点、文件系统类型和挂载选项。

## 挂载一个 ext4 分区
```bash
mount -t ext4 /dev/sdb1 /mnt/data
```
> 无输出即成功。将 `/dev/sdb1` 以 ext4 格式挂载到 `/mnt/data`，之后可通过该路径访问磁盘内容。

## 以只读方式挂载
```bash
mount -o ro /dev/sdc1 /mnt/readonly
```
> `-o ro` 只读挂载，保护原始数据不被意外修改，常用于数据恢复或取证场景。

## 挂载 ISO 镜像文件
```bash
mount -o loop ubuntu.iso /mnt/iso
```
> `-o loop` 将 ISO 文件作为回环设备挂载，无需刻录光盘即可访问镜像内容。

## 卸载设备
```bash
umount /mnt/data
```
> 无输出即成功。卸载前确保无进程占用该挂载点，否则会报 "target is busy"。

## 卸载被占用的设备（懒卸载）
```bash
umount -l /mnt/data
```
> `-l` 懒卸载：立即从目录树中移除，等设备不忙时内核自动完成清理，适合无法正常卸载的场景。
