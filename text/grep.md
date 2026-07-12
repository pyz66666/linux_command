# grep

## 在文件中搜索关键字
```bash
grep "ERROR" app.log
```
```
2025-07-12 08:30:01 ERROR Database connection failed
2025-07-12 09:15:22 ERROR Timeout sending email
```
> 输出所有包含 `ERROR` 的行，默认区分大小写。

## 搜索并显示行号
```bash
grep -n "ERROR" app.log
```
```
15:2025-07-12 08:30:01 ERROR Database connection failed
42:2025-07-12 09:15:22 ERROR Timeout sending email
```
> `-n` 在每行前加上行号，方便定位。

## 递归搜索目录
```bash
grep -r "timeout" /var/log/
```
```
/var/log/app/app.log:2025-07-12 09:15:22 ERROR Timeout sending email
/var/log/nginx/error.log:2025/07/10 14:22:10 timeout connecting to upstream
```
> `-r` 递归搜索目录下所有文件，输出格式为 `文件路径:匹配行`。

## 忽略大小写搜索
```bash
grep -ri "error" /var/log/
```
```
/var/log/app/app.log:2025-07-12 08:30:01 ERROR Database connection failed
/var/log/syslog:Jul 10 14:22 error: disk space low
```
> `-i` 忽略大小写，`ERROR` 和 `error` 都会被匹配。

## 反向匹配（排除包含关键字的行）
```bash
grep -v "DEBUG" app.log | head -3
```
```
2025-07-12 08:30:01 INFO Server started
2025-07-12 08:30:01 ERROR Database connection failed
2025-07-12 09:15:22 ERROR Timeout sending email
```
> `-v` 输出不包含 `DEBUG` 的行，排除了调试日志。

## 只显示匹配的文件名
```bash
grep -rl "TODO" ./src/
```
```
./src/main.py
./src/utils.py
```
> `-l` 只输出包含匹配内容的文件名，不显示具体内容。

## 统计匹配行数
```bash
grep -c "200" nginx_access.log
```
```
4523
```
> `-c` 输出匹配行的数量，`200` 状态码出现了 4523 次。

## 显示匹配行的上下文
```bash
grep -C 1 "ERROR" app.log
```
```
2025-07-12 08:30:00 INFO Processing request
2025-07-12 08:30:01 ERROR Database connection failed
2025-07-12 08:30:02 WARN Retrying in 5 seconds
```
> `-C 1` 显示匹配行前后各 1 行上下文，快速了解错误前后发生了什么。
