# lscpu

## 查看 CPU 完整信息
```bash
lscpu
```
```
Architecture:             x86_64
CPU(s):                   8
  On-line CPU(s) list:    0-7
Vendor ID:                GenuineIntel
  Model name:             Intel(R) Core(TM) i7-10700 CPU @ 2.90GHz
    Thread(s) per core:   2
    Core(s) per socket:   4
    Socket(s):            1
    CPU max MHz:          4800.0000
    CPU min MHz:          800.0000
Caches (sum of all):
  L1d:                    128 KiB (4 instances)
  L1i:                    128 KiB (4 instances)
  L2:                     1 MiB (4 instances)
  L3:                     16 MiB (1 instance)
NUMA:
  NUMA node(s):           1
  NUMA node0 CPU(s):      0-7
```
> 4 核 8 线程（超线程开启），基准频率 2.9GHz 睿频最高 4.8GHz，L3 缓存 16MB，单 NUMA 节点。

## 以 CSV 格式导出 CPU 映射
```bash
lscpu -p=cpu,core,socket,node
```
```
# CPU,Core,Socket,Node
0,0,0,0
1,0,0,0
2,1,0,0
3,1,0,0
4,2,0,0
5,2,0,0
6,3,0,0
7,3,0,0
```
> CPU 0 和 1 共享 Core 0（超线程对），所有 CPU 都在 Socket 0 和 Node 0（单路单 NUMA）。

## 以可解析列表格式输出
```bash
lscpu -e
```
```
CPU NODE SOCKET CORE L1d:L1i:L2:L3 ONLINE MAXMHZ    MINMHZ
  0    0      0    0 0:0:0:0       yes    4800.0000 800.0000
  1    0      0    0 0:0:0:0       yes    4800.0000 800.0000
  2    0      0    1 1:1:1:0       yes    4800.0000 800.0000
```
> `-e` 扩展列表格式，直观展示每个逻辑 CPU 对应的物理核、NUMA 节点、缓存索引和频率范围。

## 以 JSON 格式输出
```bash
lscpu -J | python3 -m json.tool | head -20
```
```
{
   "lscpu": [
      {"field": "Architecture:", "data": "x86_64"},
      {"field": "CPU(s):", "data": "8"},
      {"field": "Thread(s) per core:", "data": "2"},
      {"field": "Core(s) per socket:", "data": "4"}
   ]
}
```
> `-J` JSON 格式输出方便程序解析和自动化处理。

## 查看 NUMA 和缓存拓扑
```bash
lscpu --caches
```
```
NAME ONE-SIZE ALL-SIZE WAYS TYPE        LEVEL SETS PHY-LINE COHERENCY-SIZE
L1d      32K     128K    8 Data            1   64        1             64
L1i      32K     128K    8 Instruction     1   64        1             64
L2      256K       1M    4 Unified         2 1024        1             64
L3        4M      16M   16 Unified         3 8192        1             64
```
> `--caches` 显示每级缓存的单实例大小和总大小、相联度、缓存行大小等详细参数。
