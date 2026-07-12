# strace

## 查看命令打开了哪些文件
```bash
strace -e trace=open,openat cat /etc/hostname 2>&1
```
```
openat(AT_FDCWD, "/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libc.so.6", O_RDONLY|O_CLOEXEC) = 3
openat(AT_FDCWD, "/etc/hostname", O_RDONLY) = 3
```
> 追踪进程依次打开了动态链接器缓存、libc 库、最后才是目标文件，返回值 `= 3` 是分配的文件描述符编号。

## 统计系统调用开销
```bash
strace -c ls /tmp
```
```
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
 49.23    0.000231          11        21           mmap
 18.76    0.000088           8        11           close
 12.15    0.000057           9         6           openat
  8.53    0.000040          10         4           mprotect
  2.99    0.000014           7         2           write
------ ----------- ----------- --------- --------- ----------------
100.00    0.000469          10        48           total
```
> `-c` 统计模式汇总每种系统调用的次数和耗时，mmap 占时最多说明共享库映射是主要开销。

## 跟踪运行中进程的网络系统调用
```bash
sudo strace -p $(pgrep nginx | head -1) -e trace=network
```
```
accept4(6, {sa_family=AF_INET, sin_port=htons(54321), sin_addr=inet_addr("192.168.1.100")}, [16], SOCK_NONBLOCK) = 12
recvfrom(12, "GET / HTTP/1.1\r\nHost: example.c"..., 1024, 0, NULL, NULL) = 256
sendto(12, "HTTP/1.1 200 OK\r\nContent-Length:"..., 1024, 0, NULL, 0) = 512
close(12)                               = 0
```
> `-p` 附加到运行中的 nginx 进程，`-e trace=network` 只看网络调用，完整展示了一次 HTTP 请求处理过程。

## 跟踪子进程
```bash
strace -f -e trace=file nginx -t 2>&1
```
```
[pid 12345] openat(AT_FDCWD, "/etc/nginx/nginx.conf", O_RDONLY) = 3
[pid 12346] openat(AT_FDCWD, "/etc/nginx/mime.types", O_RDONLY) = 3
```
> `-f` 跟踪子进程，能同时看到 nginx 主进程和 worker 进程的文件操作。

## 只显示失败的系统调用
```bash
strace -e trace=file -Z cat /nonexistent 2>&1
```
```
openat(AT_FDCWD, "/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
openat(AT_FDCWD, "/nonexistent", O_RDONLY) = -1 ENOENT (No such file or directory)
```
> `-Z` 只显示失败的系统调用，快速定位"文件找不到"类问题的根因。
