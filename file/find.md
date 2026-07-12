# find

## 按文件名查找
```bash
find . -name "*.log"
```
```
./app/server.log
./nginx/access.log
./nginx/error.log
```
> 在当前目录及子目录中递归查找所有 `.log` 文件，输出为相对路径。

## 限制查找深度
```bash
find . -maxdepth 1 -name "*.conf"
```
```
./app.conf
```
> `-maxdepth 1` 只查当前目录，不进入子目录。

## 按类型查找
```bash
find /var/log -type d
```
```
/var/log/nginx
/var/log/mysql
```
> `-type d` 只输出目录，`-type f` 只输出普通文件。

## 按大小查找
```bash
find /var/log -type f -size +100M
```
```
/var/log/app/app.log
/var/log/syslog.1
```
> `+100M` 表示大于 100MB，`-100M` 小于，`100M` 等于。

## 按时间查找
```bash
find /tmp -mtime -7
```
```
/tmp/cache/abc123
/tmp/session_001
```
> `-mtime -7` 最近 7 天内修改过的文件，`+7` 表示 7 天前修改的。

## 查找并删除
```bash
find /tmp -name "*.tmp" -mtime +3 -delete
```
> 无输出即成功。删除 `/tmp` 下 3 天前修改的 `.tmp` 文件，`-delete` 要慎重。

## 查找并对结果执行命令
```bash
find . -name "*.java" -exec grep -l "TODO" {} +
```
```
./src/main/App.java
./src/util/Helper.java
```
> `-exec ... {} +` 将匹配文件批量传给 `grep`，比 `\;` 逐个执行效率高。
