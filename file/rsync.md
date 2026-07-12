# rsync

## 本地增量同步目录
```bash
rsync -avP /data/project/ /backup/project/
```
```
sending incremental file list
./
main.py
        2,048 100%    0.00kB/s    0:00:00 (xfr#1, to-chk=3/5)
utils.py
        1,536 100%    1.50MB/s    0:00:00 (xfr#2, to-chk=2/5)
config.yaml
          256 100%  256.00kB/s    0:00:00 (xfr#3, to-chk=1/5)

sent 3,840 bytes  received 76 bytes  7,832.00 bytes/sec
```
> `-a` 归档模式保留属性，`-v` 显示详情，`-P` 显示进度且支持断点续传。

## 远程同步到服务器
```bash
rsync -avzP ./deploy/ user@server:/var/www/app/
```
```
sending incremental file list
index.html
       12,500 100%    2.50MB/s    0:00:00 (xfr#1, to-chk=2/5)
style.css
        5,120 100%    1.00MB/s    0:00:00 (xfr#2, to-chk=1/5)
```
> `-z` 传输时压缩，节省带宽；源路径末尾 `/` 表示同步目录内部内容。

## 模拟运行（预览会做什么）
```bash
rsync -avn --delete ./src/ ./dst/
```
```
sending incremental file list
deleting old_feature.py
./
main.py
utils.py
```
> `-n` 模拟运行不实际执行，`--delete` 会删除目标端多余文件。

## 镜像备份（精确同步）
```bash
rsync -a --delete /source/ /mirror/
```
```
```
> `--delete` 确保目标端与源端完全一致，删除目标端多出的文件。

## 排除特定文件
```bash
rsync -av --exclude='*.log' --exclude='.git/' ./project/ /backup/
```
```
sending incremental file list
src/
src/main.py
README.md
```
> `--exclude` 跳过匹配模式的文件和目录，`.log` 文件和 `.git` 目录被排除。

## 从远程拉取
```bash
rsync -avz user@server:/var/log/nginx/ ./logs/
```
```
receiving incremental file list
access.log
error.log
```
> 远程路径在前表示从远程下载，本地路径在后表示下载目标。
