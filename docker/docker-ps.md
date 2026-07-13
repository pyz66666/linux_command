# docker ps

## 查看运行中的容器
```bash
docker ps
```
```
CONTAINER ID   IMAGE          STATUS          PORTS                  NAMES
d3f7a8b9c1e2   nginx:alpine   Up 2 hours      0.0.0.0:8080->80/tcp   web
a9b8c7d6e5f4   mysql:8        Up 30 minutes   3306/tcp               db
```
> 默认只显示正在运行的容器，CONTAINER ID 是标识、STATUS 显示运行时长、PORTS 显示端口映射。

## 查看所有容器包括已停止的
```bash
docker ps -a
```
```
CONTAINER ID   IMAGE          STATUS                      NAMES
d3f7a8b9c1e2   nginx:alpine   Up 2 hours                  web
f6e5d4c3b2a1   myapp:v1       Exited (1) 10 minutes ago   app
```
> `-a` 显示所有容器，状态 `Exited (1)` 表示非正常退出，括号内是退出码。

## 只显示容器 ID
```bash
docker ps -q
```
```
d3f7a8b9c1e2
a9b8c7d6e5f4
```
> `-q` 只输出容器 ID，适合配合 `docker rm $(docker ps -aq)` 批量删除。

## 查看最近创建的容器
```bash
docker ps -l
```
```
CONTAINER ID   IMAGE      STATUS                     NAMES
a1b2c3d4e5f6   alpine     Exited (0) 1 minute ago    cool_bell
```
> `-l` 只显示最近创建的 1 个容器，无论是否在运行。
