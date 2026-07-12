# Linux Command 速查手册

个人 Linux 命令速查库，按功能场景分类组织。每个命令一个 `.md` 文件，格式统一，方便快速定位和回顾。

## 分类索引

| 目录 | 定位 | 常用命令 |
|------|------|----------|
| [file/](file/INDEX.md) | 文件操作、归档、传输 | `ls` `cp` `mv` `find` `tar` `gzip` `rsync` `scp` |
| [text/](text/INDEX.md) | 文本处理与编辑 | `grep` `sed` `awk` `cut` `sort` `uniq` `jq` |
| [process/](process/INDEX.md) | 进程管理与服务 | `ps` `top` `kill` `systemctl` `crontab` |
| [disk-io/](disk-io/INDEX.md) | 磁盘、存储与 I/O | `df` `du` `iostat` `dd` `fio` `iozone` `mount` |
| [network/](network/INDEX.md) | 网络诊断与工具 | `curl` `ss` `ping` `tcpdump` `nmap` `dig` |
| [perf-debug/](perf-debug/INDEX.md) | 性能分析与调试 | `perf` `strace` `vmstat` `sar` `dmesg` |
| [system/](system/INDEX.md) | 系统信息与管理 | `uname` `lscpu` `lspci` `journalctl` |
| [security-perm/](security-perm/INDEX.md) | 权限控制与安全 | `chmod` `chown` `sudo` `iptables` `ssh-keygen` |

## 命令文件格式

参考 [TEMPLATE.md](TEMPLATE.md)，每个命令文件包含：
- 简介（一句话说清楚）
- 常用选项表
- 常用示例（实际能跑的）
- 注意事项（踩过的坑）

## 使用方法

```bash
# 按分类浏览
ls file/

# 全文搜索
grep -r "find . -name" .

# 搜索某个分类
grep -r "tcpdump" network/
```
