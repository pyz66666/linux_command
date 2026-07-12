# stat

## 查看文件完整元数据
```bash
stat app.log
```
```
  File: app.log
  Size: 4096     	Blocks: 8          IO Block: 4096   regular file
Device: 259,2	Inode: 1180235    Links: 1
Access: (0644/-rw-r--r--)  Uid: ( 1000/   alice)   Gid: ( 1000/   devs)
Access: 2025-07-12 10:30:25.123456789 +0800
Modify: 2025-07-12 10:28:00.987654321 +0800
Change: 2025-07-12 10:28:00.987654321 +0800
 Birth: 2025-07-10 08:00:00.000000000 +0800
```
> 显示 inode、权限、三个时间戳等所有元数据，比 `ls -l` 更详细。

## 自定义提取字段
```bash
stat -c "Size: %s bytes, Modified: %y" app.log
```
```
Size: 4096 bytes, Modified: 2025-07-12 10:28:00.987654321 +0800
```
> `-c` 自定义输出格式，`%s` 为字节大小，`%y` 为修改时间。

## 只取文件大小（适合脚本）
```bash
stat -c %s app.log
```
```
4096
```
> 输出纯数字，无额外字符，可直接赋值给 shell 变量。

## 查看文件系统信息
```bash
stat -f /
```
```
  File: "/"
    ID: 1234567890abcdef Namelen: 255     Type: ext2/ext3
Block size: 4096       Fundamental block size: 4096
Blocks: Total: 12288000  Free: 8256000   Available: 7800000
Inodes: Total: 3120000   Free: 2900000
```
> `-f` 显示挂载点所在文件系统的信息，而非文件本身。

## 简洁模式（一行输出）
```bash
stat -t app.log
```
```
app.log 4096 8 81a4 1000 1000 259 1180235 1 0 0 1752285005 1752284880 1752284880 1752105600 4096
```
> `-t` 单行输出所有数据，空格分隔，适合脚本解析。
