# scp

## 从本地上传文件到远程
```bash
scp myfile.txt user@192.168.1.100:/home/user/
```
```
myfile.txt              100%  125MB  12.5MB/s   00:10
```
> 文件完整传输到远程服务器的 `/home/user/` 目录。

## 从远程下载目录到本地
```bash
scp -r user@server:/var/log/nginx/ ./logs/
```
```
access.log               100%   45MB  10.0MB/s   00:04
error.log                100%  256KB 256.0KB/s   00:01
```
> `-r` 递归复制整个目录及其所有子文件。

## 指定非标准端口
```bash
scp -P 2222 deploy.tar.gz admin@server:/opt/deploy/
```
```
deploy.tar.gz            100%   50MB  12.5MB/s   00:04
```
> `-P`（大写）指定 SSH 端口，与 ssh 的 `-p`（小写）不同。

## 传输时压缩
```bash
scp -C large_dump.sql user@server:/backup/
```
```
large_dump.sql           100%  500MB  20.0MB/s   00:25
```
> `-C` 传输时启用压缩，适合网络较慢的场景。

## 保留文件属性
```bash
scp -p script.sh user@server:/usr/local/bin/
```
```
script.sh                100%   2KB   1.0MB/s   00:00
```
> `-p`（小写）保留源文件的修改时间和权限。

## 使用指定私钥
```bash
scp -i ~/.ssh/deploy_key app.jar deploy@server:/opt/app/
```
```
app.jar                  100%  120MB  15.0MB/s   00:08
```
> `-i` 指定用于认证的 SSH 私钥文件。
