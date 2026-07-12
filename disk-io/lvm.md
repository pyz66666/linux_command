# lvm

## 查看物理卷
```bash
sudo pvs
```
```
  PV         VG      Fmt  Attr  PSize    PFree
  /dev/sdb1  vg_data lvm2 a--  <200.00g <50.00g
  /dev/sdc1  vg_data lvm2 a--  <300.00g       0
```
> `PFree` 是该物理卷上尚未分配的空间，`<50.00g` 表示还有约 50GB 可用于扩容或新建 LV。

## 查看卷组
```bash
sudo vgs
```
```
  VG      #PV #LV #SN Attr   VSize    VFree
  vg_data   2   3   1 wz--n- <500.00g <50.00g
```
> `#PV=2` 两个物理卷组成该 VG，`VFree` 是整个卷组剩余空间，`#SN=1` 表示有一个快照。

## 查看逻辑卷
```bash
sudo lvs
```
```
  LV         VG      Attr       LSize   Pool Origin Data%  Move
  lv_mysql   vg_data -wi-ao---- 150.00g
  lv_web     vg_data -wi-ao----  50.00g
  lv_backup  vg_data -wi-a----- 250.00g
```
> `-wi-ao----` 中 `o` 表示 LV 已打开（挂载中），`LSize` 是当前逻辑卷大小。

## 在线扩容逻辑卷
```bash
sudo lvextend -L +50G /dev/vg_data/lv_mysql
sudo resize2fs /dev/vg_data/lv_mysql
```
```
  Size of logical volume vg_data/lv_mysql changed from 150.00 GiB to 200.00 GiB.
  Logical volume vg_data/lv_mysql successfully resized.
resize2fs 1.46.5 (30-Dec-2021)
Filesystem at /dev/vg_data/lv_mysql is mounted on /data/mysql; on-line resizing required
The filesystem on /dev/vg_data/lv_mysql is now 52428800 (4k) blocks long.
```
> 先 `lvextend` 扩展 LV，再 `resize2fs` 扩展文件系统，两步完全在线无需卸载。

## 创建快照用于备份
```bash
sudo lvcreate -s -L 10G -n lv_mysql_snap /dev/vg_data/lv_mysql
sudo mount -o ro /dev/vg_data/lv_mysql_snap /mnt/snap
```
```
  Logical volume "lv_mysql_snap" created.
```
> 快照是某时刻的数据冻结副本，`-L 10G` 预留 10GB 存放快照期间的数据变更，备份完成后删除快照即可。
