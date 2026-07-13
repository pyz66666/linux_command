# docker compose

## 启动多容器服务
```bash
docker compose up -d
```
```
[+] Running 3/3
 ✔ Container app-db-1   Started
 ✔ Container app-api-1  Started
 ✔ Container app-web-1  Started
```
> 读取当前目录 `docker-compose.yml`，`-d` 后台启动所有定义的服务。

## 查看服务状态
```bash
docker compose ps
```
```
NAME         IMAGE          STATUS          PORTS
app-db-1     postgres:15    Up 5 minutes    5432/tcp
app-api-1    myapp:api      Up 5 minutes    0.0.0.0:3000->3000/tcp
app-web-1    nginx:alpine   Up 5 minutes    0.0.0.0:80->80/tcp
```
> `-a` 显示所有服务（包括已停止的），比 `docker ps` 更适合查看 Compose 项目。

## 查看服务日志
```bash
docker compose logs -f api
```
```
api-1  | [2026-07-12 10:00:01] Server listening on port 3000
api-1  | [2026-07-12 10:01:05] GET /api/users 200 15ms
```
> 指定服务名 `api`，`-f` 实时跟踪，多服务时不加服务名则显示所有日志。

## 停止并删除服务
```bash
docker compose down
```
```
[+] Running 4/4
 ✔ Container app-web-1  Removed
 ✔ Container app-api-1  Removed
 ✔ Container app-db-1   Removed
 ✔ Network app_default  Removed
```
> 停止并删除所有容器和网络，`-v` 额外删除命名的数据卷。

## 重新构建并启动
```bash
docker compose up -d --build
```
```
[+] Building 15.2s
 => [api] => exporting to image  0.5s
[+] Running 3/3
...
```
> `--build` 启动前先重建镜像，代码改了又不想手动 `build` 时用。
