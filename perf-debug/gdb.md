# gdb

## 分析 core dump 文件
```bash
gdb -batch -ex "bt" -ex "info registers" ./myapp core.12345
```
```
Program terminated with signal SIGSEGV, Segmentation fault.
#0  0x00007f8a2b3c4d5e in process_request (data=0x0) at server.c:142
142         int len = strlen(data->buffer);
#1  0x00007f8a2b3c4f12 in handle_connection (fd=7) at server.c:198
#2  0x00007f8a2b3c5123 in worker_thread (arg=0x55555578a000) at server.c:245

rax            0x0                 0
rip            0x7f8a2b3c4d5e     140215678902622
```
> SIGSEGV 崩溃于 `process_request` 第 142 行，`data=0x0` 是空指针，`rax=0x0` 佐证了空指针解引用。

## 设置断点并查看变量
```bash
gdb -q ./myapp
(gdb) break process_request
(gdb) run < input.txt
(gdb) print data
(gdb) print *data
```
```
Breakpoint 1 at 0x4a2b: file server.c, line 138.

Breakpoint 1, process_request (data=0x55555578a0f0) at server.c:138
138         if (data == NULL) return -1;

(gdb) print data
$1 = (request_t *) 0x55555578a0f0

(gdb) print *data
$2 = {fd = 7, buffer = 0x55555578b010 "GET / HTTP/1.1", buflen = 16, state = 1}
```
> 断点触发后 `print *data` 展开结构体内容：fd=7、缓冲区包含 HTTP 请求、长度 16。

## 附加到运行中的进程
```bash
sudo gdb -p $(pgrep mysqld) -batch -ex "bt"
```
```
0x00007f8a2a0d4e5f in pthread_cond_wait@@GLIBC_2.3.2 () from /lib/x86_64-linux-gnu/libpthread.so.0
#0  pthread_cond_wait
#1  mysql_thread_scheduler
#2  start_thread
```
> `-p` 附加到 mysqld 进程，`bt` 查看当前调用栈，可见线程在等待条件变量（空闲状态）。

## 单步执行程序
```bash
gdb -q ./myapp
(gdb) break main
(gdb) run
(gdb) next
(gdb) step
```
```
Breakpoint 1, main () at main.c:10
10      int main() {
11          int result = parse_config("/etc/myapp.conf");
(gdb) step
parse_config (path=0x55555578a000 "/etc/myapp.conf") at config.c:5
5           FILE *f = fopen(path, "r");
```
> `next` 跳过函数调用，`step` 进入函数内部，逐行排查程序逻辑。

## 查看调用栈
```bash
gdb -batch -ex "thread apply all bt" -p $(pgrep nginx | head -1)
```
```
Thread 1 (Thread 0x7f...):
#0  sigsuspend () at ../sysdeps/unix/sysv/linux/sigsuspend.c:26
#1  ngx_master_process_cycle () at src/os/unix/ngx_process_cycle.c:139

Thread 2 (Thread 0x7f...):
#0  epoll_wait () at ../sysdeps/unix/sysv/linux/epoll_wait.c:30
#1  ngx_epoll_process_events () at src/event/modules/ngx_epoll_module.c:800
```
> `thread apply all bt` 查看所有线程的调用栈，master 线程在 sigsuspend 等待信号，worker 线程在 epoll_wait 等待事件。
