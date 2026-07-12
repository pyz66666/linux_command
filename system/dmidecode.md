# dmidecode

## 查看系统基本信息
```bash
sudo dmidecode -t system
```
```
System Information
        Manufacturer: Dell Inc.
        Product Name: XPS 15 9500
        Version: Not Specified
        Serial Number: ABC1234
        UUID: 4c4c4544-0042-3410-8032-b9c04f4a3332
        SKU Number: 097B
        Family: XPS
```
> 厂商 Dell、型号 XPS 15 9500、序列号 ABC1234（可用于保修查询）、UUID 可用于自动化部署设备识别。

## 查看内存插槽信息
```bash
sudo dmidecode -t memory
```
```
Memory Device
        Size: 8 GB
        Form Factor: SODIMM
        Locator: DIMM A
        Type: DDR4
        Speed: 3200 MT/s
        Manufacturer: Samsung
        Part Number: M471A1K43DB1-CWE

Memory Device
        Size: 8 GB
        Form Factor: SODIMM
        Locator: DIMM B
        Type: DDR4
        Speed: 3200 MT/s
```
> 两条 8GB DDR4 3200MHz SODIMM，分别插在 DIMM A 和 DIMM B 插槽，Part Number 可用于购买同型号。

## 只获取序列号
```bash
sudo dmidecode -s system-serial-number
```
```
ABC1234
```
> `-s` 只输出指定关键字的值，适合脚本中使用。

## 查看 BIOS 信息
```bash
sudo dmidecode -t bios
```
```
BIOS Information
        Vendor: Dell Inc.
        Version: 1.20.1
        Release Date: 06/15/2026
        BIOS Revision: 1.20
```
> BIOS 版本 1.20.1，发布日期 2026 年 6 月 15 日，可据此判断是否需要更新。

## 查看处理器信息
```bash
sudo dmidecode -t processor
```
```
Processor Information
        Socket Designation: U3E1
        Type: Central Processor
        Family: Core i7
        Manufacturer: Intel(R) Corporation
        Version: Intel(R) Core(TM) i7-10700 CPU @ 2.90GHz
        Max Speed: 4800 MHz
        Current Speed: 2900 MHz
        Core Count: 4
        Thread Count: 8
```
> 4 核 8 线程 i7-10700，基准 2.9GHz 最高 4.8GHz，当前运行在 2.9GHz。
