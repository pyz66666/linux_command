# sysctl

## 查看网络相关内核参数
```bash
sysctl -a | grep net.ipv4
```
```
net.ipv4.ip_forward = 0
net.ipv4.tcp_fin_timeout = 60
net.ipv4.tcp_keepalive_time = 7200
net.ipv4.tcp_max_syn_backlog = 4096
net.ipv4.tcp_syncookies = 1
net.ipv4.tcp_tw_reuse = 1
net.ipv4.conf.all.rp_filter = 1
net.ipv4.icmp_echo_ignore_all = 0
```
> `tcp_syncookies=1` SYN cookie 已启用防 SYN flood，`ip_forward=0` 未开启路由转发。

## 临时开启 IP 转发
```bash
sudo sysctl -w net.ipv4.ip_forward=1
```
```
net.ipv4.ip_forward = 1
```
> `-w` 临时修改（重启失效），让本机可以充当路由器转发 IP 包。

## 从配置文件批量加载
```bash
sudo sysctl -p /etc/sysctl.d/99-custom.conf
```
```
net.core.somaxconn = 4096
vm.swappiness = 10
kernel.pid_max = 65536
```
> `-p` 加载配置文件中的参数；somaxconn=4096 提高 TCP 监听队列，swappiness=10 减少 swap 倾向。

## 只获取单个参数值
```bash
sysctl -n net.ipv4.ip_forward
```
```
0
```
> `-n` 只输出值不显示参数名，适合脚本中使用：`[ "$(sysctl -n net.ipv4.ip_forward)" -eq 1 ]`。

## 查看所有内核参数
```bash
sysctl -a | head -10
```
```
abi.vsyscall32 = 1
debug.exception-trace = 1
dev.cdrom.autoclose = 1
dev.cdrom.check_media = 0
dev.hpet.max-user-freq = 64
dev.mac_hid.mouse_button2_keycode = 97
dev.scsi.logging_level = 0
fs.aio-max-nr = 65536
fs.aio-nr = 0
```
> `-a` 列出所有可调参数（通常上千个），结合 grep 过滤目标分类。
