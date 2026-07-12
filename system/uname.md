# uname

## 查看完整系统信息
```bash
uname -a
```
```
Linux my-server 6.5.0-14-generic #14-Ubuntu SMP PREEMPT_DYNAMIC Mon Jul  6 10:30:00 UTC 2026 x86_64 x86_64 x86_64 GNU/Linux
```
> 内核名称 Linux、主机名 my-server、内核版本 6.5.0-14、x86_64 架构、操作系统 GNU/Linux。

## 只查看内核版本
```bash
uname -r
```
```
6.5.0-14-generic
```
> 常用于脚本中判断内核版本，如 `[ "$(uname -r | cut -d. -f1)" -ge 5 ]`。

## 查看硬件架构
```bash
uname -m
```
```
x86_64
```
> `x86_64` 表示 64 位 x86，其他常见值：`aarch64`（ARM 64）、`armv7l`（ARM 32）、`riscv64`。

## 查看内核名称
```bash
uname -s
```
```
Linux
```
> 默认输出内核名称，几乎所有 Unix-like 系统都可以用这个命令跨平台判断操作系统类型。

## 查看主机名
```bash
uname -n
```
```
my-server
```
> 显示网络主机名，等同于 `hostname` 命令的输出。
