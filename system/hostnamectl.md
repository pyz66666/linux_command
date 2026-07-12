# hostnamectl

## 查看当前主机名信息
```bash
hostnamectl status
```
```
   Static hostname: my-server
         Icon name: computer-laptop
           Chassis: laptop
        Machine ID: a1b2c3d4e5f67890abcdef1234567890
           Boot ID: 1234567890abcdef1234567890abcdef
  Operating System: Ubuntu 24.04 LTS
            Kernel: Linux 6.5.0-14-generic
      Architecture: x86-64
   Hardware Vendor: Dell Inc.
    Hardware Model: XPS 15 9500
```
> 静态主机名 my-server、OS Ubuntu 24.04 LTS、硬件 Dell XPS 15 9500、Machine ID 是系统唯一标识。

## 修改主机名
```bash
sudo hostnamectl set-hostname prod-web-01
```
> 无输出即成功，同时更新 `/etc/hostname` 和内核中的主机名，新终端可见变化。

## 设置带友好名称的主机名
```bash
sudo hostnamectl set-hostname "Production Web Server 01" --pretty
hostnamectl status
```
```
   Static hostname: prod-web-01
   Pretty hostname: Production Web Server 01
```
> `--pretty` 设置显示用的友好名称，不影响网络标识。

## 设置设备类型
```bash
sudo hostnamectl set-chassis server
hostnamectl | grep Chassis
```
```
           Chassis: server
```
> 将设备类型标记为 server（可选值：desktop、laptop、server、tablet、vm 等）。

## 查看内核主机名
```bash
cat /proc/sys/kernel/hostname
```
```
prod-web-01
```
> 直接读取内核参数验证主机名已生效，等同于 `hostname` 命令。
