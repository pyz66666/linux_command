# perf

## 统计程序性能计数器
```bash
perf stat ls -R /usr/share > /dev/null
```
```
 Performance counter stats for 'ls -R /usr/share':

          1,245.38 msec task-clock                #    0.997 CPUs utilized
                45      context-switches          #   36.134 /sec
                 2      cpu-migrations            #    1.606 /sec
               512      page-faults               #  411.071 /sec
     3,201,456,789      cycles                    #    2.571 GHz
     2,100,345,678      instructions              #    0.66  insn per cycle
       420,123,456      branches                  #  337.321 M/sec
        12,345,678      branch-misses             #    2.94% of all branches

       1.249012345 seconds time elapsed
```
> `perf stat` 统计 CPU 周期、指令数、分支预测等硬件性能计数器，IPC 0.66 偏低提示可能受 cache miss 影响。

## 采样 CPU 热点并生成报告
```bash
perf record -g ./my_program
perf report
```
```
Samples: 10K of event 'cycles', Event count (approx.): 8500000000
  Children      Self  Command      Shared Object       Symbol
+   45.23%     0.00%  my_program   [kernel.kallsyms]   [k] entry_SYSCALL_64
+   44.12%     1.20%  my_program   my_program          [.] compute_hash
+   38.50%     5.34%  my_program   my_program          [.] parse_json
+   25.10%    25.10%  my_program   libcrypto.so.3      [.] SHA256_Transform
```
> `-g` 记录调用栈，`perf report` 交互式查看；SHA256_Transform 的 Self=25% 说明它是叶子函数瓶颈。

## 实时查看系统 CPU 热点
```bash
sudo perf top
```
```
Samples: 12K of event 'cycles', 4000 Hz, Event count (approx.): 3200000000 lost: 0/0 drop: 0/0
Overhead  Shared Object       Symbol
  15.23%  [kernel]            [k] copy_user_enhanced_fast_string
   8.45%  libc.so.6           [.] __memmove_avx_unaligned_erms
   6.78%  mysqld              [.] my_hash_sort_utf8
```
> `perf top` 实时刷新最耗 CPU 的函数，类似 top 命令的性能版。

## 列出可用性能事件
```bash
perf list | head -10
```
```
List of pre-defined events (to be used in -e):

  branch-instructions OR branches                    [Hardware event]
  branch-misses                                      [Hardware event]
  cache-misses                                       [Hardware event]
  cache-references                                   [Hardware event]
  cpu-cycles OR cycles                               [Hardware event]
  instructions                                       [Hardware event]
```
> `perf list` 列出所有可追踪的硬件和软件事件，供 `-e` 参数选择使用。
