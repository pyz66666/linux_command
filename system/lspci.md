# lspci

## 列出所有 PCI 设备
```bash
lspci
```
```
00:00.0 Host bridge: Intel Corporation 10th Gen Core Processor Host Bridge/DRAM Registers
00:02.0 VGA compatible controller: Intel Corporation CometLake-S GT2 [UHD Graphics 630]
00:14.0 USB controller: Intel Corporation 400 Series Chipset Family USB 3.2 xHCI Controller
00:14.3 Network controller: Intel Corporation Wireless-AC 9462
00:17.0 SATA controller: Intel Corporation 400 Series Chipset Family SATA AHCI Controller
00:1f.3 Audio device: Intel Corporation 400 Series Chipset Family HD Audio Controller
01:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller PM9A1
```
> 列出了显卡（UHD 630）、无线网卡（AC 9462）、USB 控制器、SATA 控制器、NVMe SSD 等所有 PCIe 设备。

## 查看每个设备使用的内核驱动
```bash
lspci -k
```
```
00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 630
        Kernel driver in use: i915
        Kernel modules: i915

00:14.3 Network controller: Intel Corporation Wireless-AC 9462
        Kernel driver in use: iwlwifi
        Kernel modules: iwlwifi

01:00.0 Non-Volatile memory controller: Samsung NVMe SSD Controller PM9A1
        Kernel driver in use: nvme
        Kernel modules: nvme
```
> `-k` 显示驱动状态：显卡用 i915、无线网卡用 iwlwifi、NVMe 用 nvme 驱动，全部已正常加载。

## 查看 PCI 设备拓扑
```bash
lspci -t
```
```
-[0000:00]-+-00.0
           +-02.0
           +-14.0
           +-14.3
           +-17.0
           +-1f.3
           \-1c.0-[01]----00.0
```
> 树形拓扑显示 `00:1c.0` 是一个 PCIe 桥，桥后面是总线 01 上的 NVMe SSD（01:00.0）。

## 以数字形式显示厂商和设备 ID
```bash
lspci -nn | head -5
```
```
00:00.0 Host bridge [0600]: Intel Corporation 10th Gen Core Processor Host Bridge [8086:9b43] (rev 05)
00:02.0 VGA compatible controller [0300]: Intel Corporation UHD Graphics 630 [8086:9bc8] (rev 05)
00:14.3 Network controller [0280]: Intel Corporation Wireless-AC 9462 [8086:02f0]
```
> `-nn` 显示 `[vendor:product]` ID 如 `[8086:9bc8]`，可用于搜索驱动兼容性。

## 查看详细设备信息
```bash
lspci -v -s 00:02.0
```
```
00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 630 (prog-if 00 [VGA controller])
        Flags: bus master, fast devsel, latency 0, IRQ 130
        Memory at 6012000000 (64-bit, non-prefetchable) [size=16M]
        Memory at 4000000000 (64-bit, prefetchable) [size=256M]
        Kernel driver in use: i915
```
> `-v` 详细模式 + `-s` 指定设备地址，显示 BAR 内存映射地址和 IRQ 号。
