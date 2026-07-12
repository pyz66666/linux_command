# dmesg

## 查看最近的错误和警告
```bash
dmesg -T -l err,warn | tail -20
```
```
[Mon Jul 12 09:23:15 2026] ACPI Error: No handler for Region [ECRM] (20230331/evregion-130)
[Mon Jul 12 09:23:15 2026] Bluetooth: hci0: unexpected event for opcode 0x0c03
[Mon Jul 12 09:23:16 2026] iwlwifi 0000:00:14.3: WRT: Invalid buffer destination
[Mon Jul 12 09:23:18 2026] mce: CPU0: Core temperature above threshold, cpu clock throttled
```
> 过滤出 error 和 warn 级别的内核日志，快速定位硬件/驱动问题。

## 实时监控内核日志
```bash
dmesg -wH
```
```
kern  :info : [Mon Jul 12 09:30:01 2026] usb 1-2: new high-speed USB device number 5 using xhci_hcd
kern  :info : [Mon Jul 12 09:30:01 2026] usb 1-2: New USB device found, idVendor=0781, idProduct=5583
kern  :info : [Mon Jul 12 09:30:01 2026] usb-storage 1-2:1.0: USB Mass Storage device detected
```
> `-w` 持续跟踪新日志（类似 tail -f），`-H` 彩色人类可读格式，可以看到设备热插拔时内核的识别过程。

## 只查看内核消息
```bash
dmesg -k | tail -10
```
```
[    3.456789] EXT4-fs (sda1): mounted filesystem with ordered data mode
[    4.123456] nvme nvme0: 8/0/0 default/read/poll queues
[    5.789012] e1000e: eth0 NIC Link is Up 1000 Mbps Full Duplex
```
> `-k` 只显示内核消息，排除用户态日志。

## 搜索特定关键词
```bash
dmesg | grep -i usb
```
```
[    1.234567] usbcore: registered new interface driver usb-storage
[    1.345678] usb 1-1: new high-speed USB device number 2 using xhci_hcd
[    1.456789] usb 1-1: New USB device found, idVendor=0781, idProduct=5583
```
> 用 grep 过滤关键词快速定位 USB 相关问题。

## 清空环形缓冲区
```bash
sudo dmesg -C
```
> 无输出即成功，清空后 `dmesg` 将只显示新产生的日志，方便测试时观察增量输出。
