# timedatectl

## 查看当前时间和时区状态
```bash
timedatectl status
```
```
               Local time: 一 2026-07-12 10:35:42 CST
           Universal time: 一 2026-07-12 02:35:42 UTC
                 RTC time: 一 2026-07-12 10:35:42
                Time zone: Asia/Shanghai (CST, +0800)
System clock synchronized: yes
              NTP service: active
          RTC in local TZ: yes
```
> 时区为 Asia/Shanghai（UTC+8），NTP 同步已启用且同步成功，RTC 使用本地时间（Windows 双系统常见）。

## 设置时区
```bash
sudo timedatectl set-timezone Asia/Shanghai
```
> 无输出即成功，将系统时区设置为东八区。

## 启用 NTP 自动同步
```bash
sudo timedatectl set-ntp true
```
> 启用 systemd-timesyncd 自动同步网络时间，确保系统时钟准确。

## 列出可用时区
```bash
timedatectl list-timezones | grep -i "tokyo\|new_york"
```
```
America/New_York
Asia/Tokyo
```
> `list-timezones` 列出所有可用时区，用 grep 筛选目标城市。

## 查看 NTP 同步详情
```bash
timedatectl show-timesync
```
```
SystemNTPServers=ntp.ubuntu.com
FallbackNTPServers=ntp.ubuntu.com
ServerName=ntp.ubuntu.com
ServerAddress=91.189.91.157
RootDistanceMaxUSec=5s
PollIntervalMinUSec=32s
PollIntervalMaxUSec=34min 8s
Frequency=0
```
> `show-timesync` 显示 NTP 服务器地址、轮询间隔等详细同步参数。
