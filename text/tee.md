# tee

## 同时输出到屏幕和文件
```bash
./run.sh | tee output.log
```
```
Starting application...
Loading configuration...
Server listening on port 8080
```
> 命令输出既显示在终端又写入 `output.log`，适合边看边记录。

## 追加到日志文件
```bash
python app.py 2>&1 | tee -a app.log
```
```
2025-07-12 10:30:00 App started
2025-07-12 10:30:05 Processing request
```
> `-a` 追加模式不覆盖原文件，`2>&1` 合并 stderr 和 stdout。

## 写入多个文件
```bash
make | tee build.log errors.log
```
```
gcc -c main.c -o main.o
gcc -c utils.c -o utils.o
gcc main.o utils.o -o app
```
> 同时写入 `build.log` 和 `errors.log` 两个文件。

## 使用 sudo 写文件
```bash
echo "server_name example.com;" | sudo tee -a /etc/nginx/nginx.conf
```
```
server_name example.com;
```
> 普通用户管道给 `sudo tee`，突破权限限制写入系统文件。

## 分流到多个子进程
```bash
cat data.csv | tee >(wc -l) >(head -3) > /dev/null
```
```
3
id,name,score
1,Alice,95
2,Bob,72
```
> 进程替换 `>(cmd)` 将数据同时发送给 `wc -l` 和 `head -3` 两个子进程。
