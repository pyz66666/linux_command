# fsck

## 检查文件系统（只读，不修复）
```bash
sudo fsck.ext4 -n /dev/sdb1
```
```
e2fsck 1.46.5 (30-Dec-2021)
/dev/sdb1: clean, 150234/6553600 files, 5123400/26214400 blocks
```
> `clean` 表示文件系统状态正常，`-n` 只检查不修复，安全无副作用。

## 检查并自动修复文件系统
```bash
sudo fsck.ext4 -y /dev/sdb1
```
```
e2fsck 1.46.5 (30-Dec-2021)
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information

/dev/sdb1: ***** FILE SYSTEM WAS MODIFIED *****
/dev/sdb1: 150234/6553600 files (0.2% non-contiguous), 5123400/26214400 blocks
```
> 5 个 Pass 逐步检查 inode、目录结构、连通性、引用计数、块位图；`MODIFIED` 表示修复了问题。

## 强制检查（即使标记为 clean）
```bash
sudo fsck.ext4 -f /dev/sda1
```
```
e2fsck 1.46.5 (30-Dec-2021)
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information

/dev/sda1: 320156/3276800 files (0.1% non-contiguous), 8956400/13107200 blocks
```
> `-f` 强制检查，即使文件系统标记为 clean 也会完整走一遍 5 个 Pass。

## 检查 XFS 文件系统
```bash
sudo xfs_repair -n /dev/sdb1
```
```
Phase 1 - find and verify superblock...
Phase 2 - using internal log
Phase 3 - for each AG...
        - scan and clear agi unlinked lists...
Phase 4 - check for duplicate blocks...
Phase 5 - rebuild AG headers and trees...
Phase 6 - check inode connectivity...
Phase 7 - verify link counts...
No modify flag set, skipping filesystem flush and exiting.
```
> XFS 用 `xfs_repair -n` 只读检查，去掉 `-n` 即执行修复；必须在卸载后运行。
