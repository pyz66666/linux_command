# lsusb

## 列出所有 USB 设备
```bash
lsusb
```
```
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 003: ID 0781:5583 SanDisk Corp. Ultra Fit
Bus 002 Device 002: ID 0bda:8153 Realtek Semiconductor Corp. RTL8153 Gigabit Ethernet Adapter
Bus 001 Device 004: ID 8087:0026 Intel Corp. AX201 Bluetooth
Bus 001 Device 003: ID 0c45:672e Microdia Integrated_Webcam_HD
Bus 001 Device 002: ID 046d:c092 Logitech, Inc. G203 Gaming Mouse
```
> SanDisk U 盘、Realtek USB 网卡、Intel 蓝牙模块、集成摄像头、罗技鼠标——所有 USB 设备一览。

## 查看 USB 设备拓扑树
```bash
lsusb -t
```
```
/:  Bus 04.Port 1: Dev 1, Class=root_hub, Driver=xhci_hcd/2p, 10000M
/:  Bus 02.Port 1: Dev 1, Class=root_hub, Driver=xhci_hcd/4p, 10000M
    |__ Port 2: Dev 2, If 0, Class=Vendor Specific Class, Driver=r8152, 5000M
    |__ Port 3: Dev 3, If 0, Class=Mass Storage, Driver=usb-storage, 5000M
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=xhci_hcd/12p, 480M
    |__ Port 3: Dev 4, If 0, Class=Wireless, Driver=btusb, 12M
    |__ Port 4: Dev 2, If 1, Class=Human Interface Device, Driver=usbhid, 12M
```
> 树形结构显示各设备挂载的端口和驱动，5000M=USB 3.0、480M=USB 2.0、12M=USB 1.1。

## 查看特定厂商和产品的设备
```bash
lsusb -d 0781:5583
```
```
Bus 002 Device 003: ID 0781:5583 SanDisk Corp. Ultra Fit
```
> `-d` 按 VENDOR:PRODUCT ID 过滤，快速定位特定 U 盘设备。

## 查看特定设备的详细信息
```bash
sudo lsusb -v -d 0781:5583 2>&1 | head -20
```
```
Bus 002 Device 003: ID 0781:5583 SanDisk Corp. Ultra Fit
Device Descriptor:
  bLength                18
  bDescriptorType         1
  bcdUSB               3.10
  bDeviceClass            0
  idVendor           0x0781 SanDisk Corp.
  idProduct          0x5583 Ultra Fit
  bcdDevice            1.00
  iManufacturer           1 SanDisk
  iProduct                2 Ultra Fit
  iSerial                 3 4C530001230207110365
```
> `-v` 详细模式显示设备描述符（USB 3.1 协议、厂商字符串、序列号），需要 sudo 才能读取完整信息。

## 对比插拔前后找新设备
```bash
lsusb > /tmp/before.txt
# 插入设备...
lsusb > /tmp/after.txt
diff /tmp/before.txt /tmp/after.txt
```
```
4a5
> Bus 002 Device 004: ID 0951:1666 Kingston Technology DataTraveler 100 G3
```
> 拔插前后对比差异快速找出新插入设备的 Bus/Device 编号和 VID/PID。
