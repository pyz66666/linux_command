# slabtop

## 一次性查看内核 slab 使用排行
```bash
sudo slabtop -o -s c | head -20
```
```
 Active / Total Objects (% used)    : 2345678 / 2500000 (93.8%)
 Active / Total Slabs (% used)      : 45678 / 45800 (99.7%)
 Active / Total Caches (% used)     : 123 / 150 (82.0%)
 Active / Total Size (% used)       : 234567.89K / 250000.00K (93.8%)

  OBJS ACTIVE  USE OBJ SIZE  SLABS OBJ/SLAB CACHE SIZE NAME
345678 345000  99%    1.06K  11526       30     46080K dentry
234567 220000  93%    0.57K   8378       28     33508K inode_cache
123456 120000  97%    0.19K   5880       21     23520K kmalloc-192
 89012  85000  95%    0.25K   5564       16     22256K buffer_head
```
> `-o` 一次性输出，`-s c` 按缓存大小排序；dentry（目录项缓存）占用 46MB 最多，这是正常的内核加速行为。

## 按对象数量排序排查泄漏
```bash
sudo slabtop -o -s b
```
```
  OBJS  ACTIVE  USE OBJ SIZE  SLABS OBJ/SLAB CACHE SIZE NAME
456789  123456  27%    0.03K   3569      128     14276K kmalloc-32
345678  345000  99%    1.06K  11526       30     46080K dentry
```
> `kmalloc-32` 有 456789 个对象但仅 27% 活跃（active），大量不活跃对象暗示可能存在内核内存泄漏。

## 交互模式按指定列实时排序
```bash
sudo slabtop
```
> 进入交互界面后按 `c` 键按缓存大小排序，按 `o` 键按对象数量排序，按 `q` 退出；适合实时观察 slab 变化趋势。

## 每 3 秒刷新一次
```bash
sudo slabtop -d 3 -o -s c
```
```
 Active / Total Objects (% used)    : 2346000 / 2500000 (93.8%)
 Active / Total Size (% used)       : 234600.00K / 250000.00K (93.8%)

  OBJS ACTIVE  USE OBJ SIZE  SLABS OBJ/SLAB CACHE SIZE NAME
345700 345000  99%    1.06K  11527       30     46108K dentry
```
> `-d 3` 每 3 秒刷新一次，观察 dentry 的 OBJS 从 345678 增到 345700 说明文件访问在持续产生新缓存。

## 配合 drop_caches 释放可回收 slab
```bash
echo 2 | sudo tee /proc/sys/vm/drop_caches
sudo slabtop -o -s c | head -15
```
```
 Active / Total Objects (% used)    : 1203456 / 1350000 (89.1%)
  OBJS ACTIVE  USE OBJ SIZE  SLABS OBJ/SLAB CACHE SIZE NAME
123456 123000  99%    1.06K   4116       30     16464K dentry
 89012  88000  98%    0.57K   3180       28     12720K inode_cache
```
> `echo 2 > drop_caches` 释放 dentry/inode 缓存后，dentry 从 46MB 降到 16MB，确认缓存可正常回收。
