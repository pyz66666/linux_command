# ln

## 创建软链接指向文件
```bash
ln -s /usr/local/bin/python3.11 /usr/local/bin/python
```
```
```
> 无输出即成功，`python` 成为指向 `python3.11` 的符号链接。

## 查看软链接
```bash
ls -l /usr/local/bin/python
```
```
lrwxrwxrwx 1 root root 25 Jul 12 09:00 /usr/local/bin/python -> /usr/local/bin/python3.11
```
> 首字符 `l` 表示软链接，箭头 `->` 指向实际目标。

## 创建软链接指向目录
```bash
ln -s /data/logs/app /var/log/myapp
```
```
```
> 目录也可以创建软链接，访问 `/var/log/myapp` 相当于访问 `/data/logs/app`。

## 创建硬链接
```bash
ln original.txt hardlink.txt
```
```
```
> 两个文件名指向同一个 inode，共享数据块。

## 查看硬链接（通过 inode）
```bash
ls -li original.txt hardlink.txt
```
```
1180234 -rw-r--r-- 2 alice devs 1024 Jul 12 10:00 hardlink.txt
1180234 -rw-r--r-- 2 alice devs 1024 Jul 12 10:00 original.txt
```
> inode 号相同（1180234），链接计数 `2` 表示有两个目录条目指向该 inode。

## 强制覆盖已有链接
```bash
ln -sf /usr/bin/python3.12 /usr/local/bin/python
```
```
```
> `-f` 强制覆盖已存在的目标文件或链接，`-s` 创建软链接。
