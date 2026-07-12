# ltrace

## 查看命令调用了哪些库函数
```bash
ltrace cat /etc/hostname
```
```
getenv("POSIXLY_CORRECT")                    = nil
strrchr("cat", '/')                          = nil
setlocale(LC_ALL, "")                        = "zh_CN.UTF-8"
fopen("/etc/hostname", "r")                  = 0x55a1b2c3d4e0
fread(0x55a1b2c3d5f0, 1, 1024, 0x55a1b2c3d4e0) = 12
fwrite("my-hostname\n", 1, 12, 0x7f8a2b3c4000) = 12
fclose(0x55a1b2c3d4e0)                      = 0
```
> 追踪 cat 的 libc 调用链路：检查环境变量 → 设置本地化 → 打开文件 → 读取 12 字节 → 写入 stdout → 关闭文件。

## 统计程序的内存分配
```bash
ltrace -c -e 'malloc+free+realloc+calloc' ./myapp
```
```
% time     seconds  usecs/call     calls      function
------ ----------- ----------- --------- --------------------
 56.23    0.001234          12       100      malloc
 32.15    0.000723          10        72      free
 11.62    0.000256          18        14      realloc
------ ----------- ----------- --------- --------------------
100.00    0.002213                   186      total
```
> `-c` 统计模式：malloc 100 次但 free 只有 72 次，存在 28 次潜在内存泄漏需进一步排查。

## 附加到运行中进程查看网络调用
```bash
sudo ltrace -p $(pgrep redis-server) -e 'connect+send+recv+accept'
```
```
accept(6, 0x7ffe1234, 0x7ffe1238, 0)        = 9
recv(9, "*2\r\n$4\r\nINFO\r\n", 1024, 0)    = 15
send(9, "$876\r\n# Server\r\nredis_versio"..., 876, 0) = 876
recv(9, "*3\r\n$3\r\nSET\r\n$4\r\nkey1\r\n"..., 1024, 0) = 35
send(9, "+OK\r\n", 5, 0)                     = 5
```
> `-p` 附加到 redis-server，`-e` 只追踪网络函数：接受连接 → 收到 INFO 命令 → 返回响应 → 收到 SET 命令 → 返回 OK。

## 同时显示系统调用
```bash
ltrace -S cat /etc/hostname 2>&1 | tail -10
```
```
SYS_openat(0xffffff9c, 0x7f..., 0, 0)       = 3
fopen("/etc/hostname", "r")                  = 0x55a1b2c3d4e0
SYS_read(3, 0x55a1b2c3d5f0, 1024)           = 12
fread(0x55a1b2c3d5f0, 1, 1024, 0x55a1b2c3d4e0) = 12
```
> `-S` 同时显示库函数和底层系统调用的映射关系，fopen 对应 SYS_openat，fread 对应 SYS_read。

## 带时间戳跟踪
```bash
ltrace -tt cat /etc/hostname 2>&1
```
```
10:35:42.123456 getenv("POSIXLY_CORRECT")    = nil
10:35:42.123478 fopen("/etc/hostname", "r")  = 0x55a1b2c3d4e0
10:35:42.124012 fread(0x55a1b2c3d5f0, ...)  = 12
10:35:42.124345 fwrite("my-hostname\n", ...) = 12
10:35:42.124456 fclose(0x55a1b2c3d4e0)      = 0
```
> `-tt` 微秒级时间戳显示每个库函数调用的精确时间，fopen 到 fread 之间耗时约 0.5ms。
