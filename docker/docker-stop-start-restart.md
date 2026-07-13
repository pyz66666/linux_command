# docker start / stop / restart

## 启动已停止的容器
```bash
docker start db
```
```
db
```
> 恢复状态为 `Exited` 的容器，保留原有的端口映射和数据卷挂载。

## 重启容器
```bash
docker restart web
```
```
web
```
> 等同于 `docker stop` 再 `docker start`，常用于应用更新后重启使配置生效。

## 优雅停止容器
```bash
docker stop web
```
```
web
```
> 发送 SIGTERM 信号等待 10 秒（默认），超时未退出则发送 SIGKILL 强制终止。

## 设置超时时间停止
```bash
docker stop -t 30 web
```
```
web
```
> `-t 30` 等待 30 秒后再发 SIGKILL，给应用足够的优雅关闭时间。

## 批量停止所有运行中的容器
```bash
docker stop $(docker ps -q)
```
```
d3f7a8b9c1e2
a9b8c7d6e5f4
```
> `$(docker ps -q)` 获取所有运行中容器的 ID 列表传入 `docker stop`。
