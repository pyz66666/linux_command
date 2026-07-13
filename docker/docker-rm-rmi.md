# docker rm / rmi

## 删除已停止的容器
```bash
docker rm app
```
```
app
```
> 只能删除已停止的容器，运行中的容器需先 `stop` 或用 `-f` 强制删除。

## 强制删除运行中的容器
```bash
docker rm -f web
```
```
web
```
> `-f` 先 SIGKILL 终止再删除，跳过优雅关闭阶段。

## 批量删除所有已停止的容器
```bash
docker rm $(docker ps -aq)
```
```
d3f7a8b9c1e2
f6e5d4c3b2a1
```
> `-a` 获取所有容器 ID，传入 `docker rm` 批量清理。

## 删除镜像
```bash
docker rmi myapp:v1
```
```
Untagged: myapp:v1
Deleted: sha256:a1b2c3d4e5f6...
```
> 删除镜像的指定标签，如有多个标签指向同一镜像，只删除当前标签不删镜像层。

## 强制删除镜像
```bash
docker rmi -f myapp:latest
```
```
Untagged: myapp:latest
Deleted: sha256:a1b2c3d4e5f6...
```
> `-f` 强制删除，即使有容器引用了该镜像。

## 清理无用资源
```bash
docker system prune -a
```
```
Deleted Containers:
d3f7a8b9c1e2
Deleted Images:
myapp:v1
Total reclaimed space: 1.2GB
```
> 删除所有已停止的容器、未使用的网络、悬空镜像，`-a` 连未被容器引用的镜像也删。
