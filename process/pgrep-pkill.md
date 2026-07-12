# pgrep / pkill

## 按进程名查找 PID
```bash
pgrep nginx
```
```
1234
1235
1236
1237
1238
```
> 输出所有 nginx 进程的 PID，1 个 master + 4 个 worker。

## 查找并显示进程名
```bash
pgrep -l python
```
```
12345 python
12400 python
```
> `-l` 同时显示进程名和 PID，方便区分。

## 查找并显示完整命令行
```bash
pgrep -a python
```
```
12345 python /opt/app/main.py
12400 python /opt/app/celery_worker.py
```
> `-a` 显示完整命令行参数，可区分不同的 Python 程序。

## 按完整命令行匹配
```bash
pgrep -f celery
```
```
12400
```
> `-f` 匹配完整命令行，`celery` 出现在参数中也被匹配到。

## 精确匹配进程名
```bash
pgrep -x nginx
```
```
1234
```
> `-x` 精确匹配，进程名必须完全等于 `nginx`。

## 优雅终止指定进程
```bash
pkill celery
```
```
```
> 默认发送 `SIGTERM`，终止所有名为 `celery` 的进程。

## 强制终止匹配的进程
```bash
pkill -9 -f "python app.py"
```
```
```
> `-9` 发送 `SIGKILL`，`-f` 按完整命令行匹配后强制终止。

## 按用户过滤并终止
```bash
pkill -u www-data nginx
```
```
```
> `-u` 只终止指定用户运行的进程，不会误杀其他用户的同名进程。

## 检查进程是否存活（脚本用）
```bash
pgrep -x nginx && echo "running" || echo "not running"
```
```
running
```
> 利用 `pgrep` 的退出码，适合在脚本中判断服务状态。
