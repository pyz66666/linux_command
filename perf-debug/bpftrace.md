# bpftrace

## 统计每个进程的系统调用次数
```bash
sudo bpftrace -e 'tracepoint:raw_syscalls:sys_enter { @[comm] = count(); }'
```
```
Attaching 1 probe...
^C

@[node]: 12345
@[mysqld]: 89234
@[sshd]: 2345
@[systemd-journal]: 567
```
> 在 `sys_enter` 探针点统计每个进程的 syscall 次数，mysqld 以 89234 次居首。

## 追踪进程打开的文件
```bash
sudo bpftrace -e 'tracepoint:syscalls:sys_enter_openat { printf("%s %s\n", comm, str(args->filename)); }'
```
```
Attaching 1 probe...
cat /etc/ld.so.cache
cat /lib/x86_64-linux-gnu/libc.so.6
cat /etc/hostname
nginx /var/log/nginx/access.log
python3 /home/user/data.json
```
> 在 `openat` 入口打印进程名和文件名，可以看到 cat、nginx、python3 各自打开了哪些文件。

## 统计磁盘 I/O 延迟分布
```bash
sudo bpftrace -e 'kprobe:blk_account_io_done { @usecs = hist((nsecs - @start[arg0]) / 1000); delete(@start[arg0]); } kprobe:blk_account_io_start { @start[arg0] = nsecs; }'
```
```
@usecs:
[0]                  123 |@@@@@@@@@@@@@@@@@@@@@@@@@@                          |
[1]                  234 |@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@|
[2, 4)               156 |@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@                  |
[4, 8)                67 |@@@@@@@@@@@@@@                                      |
[8, 16)               23 |@@@@@                                               |
[16, 32)               8 |@                                                   |
[32, 64)               3 |                                                    |
```
> 在 I/O 开始和完成探针记录延迟，`hist()` 生成直方图，大部分 I/O 在 1-2 微秒完成（命中缓存）。

## 追踪进程启动
```bash
sudo bpftrace -e 'tracepoint:sched:sched_process_exec { printf("PID=%d %s\n", pid, comm); }'
```
```
Attaching 1 probe...
PID=12345 bash
PID=12346 ls
PID=12347 grep
```
> `sched_process_exec` 在进程 exec 时触发，实时显示新启动的进程 PID 和名称。

## 统计 TCP 连接
```bash
sudo bpftrace -e 'kprobe:tcp_connect { @[comm] = count(); }'
```
```
Attaching 1 probe...
^C

@[curl]: 5
@[node]: 23
@[sshd]: 1
```
> 在 `tcp_connect` 内核函数处统计每个进程发起的 TCP 连接数。
