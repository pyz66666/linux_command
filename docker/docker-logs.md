# docker logs

## 查看容器日志
```bash
docker logs web
```
```
172.17.0.1 - - [12/Jul/2026:10:00:01 +0000] "GET / HTTP/1.1" 200 612
172.17.0.1 - - [12/Jul/2026:10:00:03 +0000] "GET /api/health HTTP/1.1" 200 45
```
> 输出容器内进程的所有 stdout/stderr，默认按时间顺序显示。

## 实时跟踪日志
```bash
docker logs -f web
```
```
172.17.0.1 - - [12/Jul/2026:10:01:00 +0000] "POST /api/login HTTP/1.1" 200 128
172.17.0.1 - - [12/Jul/2026:10:01:05 +0000] "GET /dashboard HTTP/1.1" 200 2048
```
> `-f` 持续跟踪（类似 `tail -f`），新日志实时输出，Ctrl+C 退出。

## 显示最近 N 行 + 时间戳
```bash
docker logs --tail 10 -t web
```
```
2026-07-12T10:00:58.123Z GET /api/health 200
2026-07-12T10:01:00.456Z POST /api/login 200
2026-07-12T10:01:05.789Z GET /dashboard 200
```
> `--tail` 只显示最后 10 行，`-t` 加上时间戳，快速定位最近的请求。

## 查看某个时间段的日志
```bash
docker logs --since 2026-07-12T09:00:00 --until 2026-07-12T10:00:00 web
```
```
172.17.0.1 - - [12/Jul/2026:09:30:00 +0000] "GET / HTTP/1.1" 200 612
```
> `--since`/`--until` 限定时间范围，适合按时间段排查问题。
