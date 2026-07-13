# docker run

## 后台运行并映射端口
```bash
docker run -d -p 8080:80 --name web nginx:alpine
```
```
d3f7a8b9c1e2
```
> `-d` 后台运行，`-p 主机:容器` 端口映射，`--name` 取名方便后续操作，返回容器 ID 短哈希。

## 交互式进入容器
```bash
docker run -it ubuntu:22.04 /bin/bash
```
```
root@a1b2c3d4e5f6:/#
```
> `-it` 分配交互终端，退出 shell 时容器会停止（因为没有前台进程了）。

## 挂载数据卷
```bash
docker run -d -v /host/data:/app/data --name app myapp:v1
```
```
f6e5d4c3b2a1
```
> `-v` 将主机目录 `/host/data` 挂载到容器的 `/app/data`，数据持久化在主机上。

## 设置环境变量
```bash
docker run -d -e MYSQL_ROOT_PASSWORD=secret -e MYSQL_DATABASE=mydb --name db mysql:8
```
```
a9b8c7d6e5f4
```
> `-e` 传入环境变量，MySQL 镜像通过这些变量自动初始化。

## 限制内存和 CPU
```bash
docker run -d --memory=512m --cpus=1.5 --name limited nginx
```
```
b1c2d3e4f5a6
```
> `--memory` 限制最大内存 512MB，`--cpus` 限制最多使用 1.5 个 CPU 核心。

## 容器退出后自动删除
```bash
docker run --rm alpine echo "done"
```
```
done
```
> `--rm` 容器退出后自动清理，适合跑一次性任务，不留垃圾。
