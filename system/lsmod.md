# lsmod

## 查看所有已加载模块
```bash
lsmod
```
```
Module                  Size  Used by
iwlwifi               385024  1
iwlmvm                356352  1 iwlwifi
mac80211             1024000  1 iwlmvm
nvidia_drm             77824  2
nvidia_modeset       1228800  1 nvidia_drm
nvidia               56532992  78 nvidia_modeset
nvme                   49152  2
xhci_hcd              307200  1 xhci_pci
ext4                  925696  1
dm_crypt               53248  1
```
> WiFi 驱动栈（iwlwifi←iwlmvm←mac80211）、NVIDIA 驱动（56MB）、NVMe 驱动、ext4 文件系统、dm_crypt 加密模块均已加载。

## 检查特定模块是否已加载
```bash
lsmod | grep nvidia
```
```
nvidia_drm             77824  2
nvidia_modeset       1228800  1 nvidia_drm
nvidia               56532992  78 nvidia_modeset
```
> 三个 NVIDIA 相关模块均已加载，如果无输出说明 NVIDIA 驱动未加载（可能 nouveau 在运行）。

## 查看模块依赖关系
```bash
lsmod | grep -E "iwlwifi|iwlmvm|mac80211|cfg80211"
```
```
iwlwifi               385024  0
iwlmvm                356352  1 iwlwifi
mac80211             1024000  1 iwlmvm
cfg80211              970752  3 iwlwifi,iwlmvm,mac80211
```
> cfg80211 被 iwlwifi、iwlmvm、mac80211 三个模块共同依赖（Used by=3），卸载需按相反顺序。

## 查看模块详细信息
```bash
modinfo nvme
```
```
filename:       /lib/modules/6.5.0-14-generic/kernel/drivers/nvme/host/nvme.ko
version:        1.0
license:        GPL
description:    NVMe host driver
author:         Matthew Wilcox <willy@linux.intel.com>
depends:        nvme-core
```
> `modinfo` 显示模块的文件路径、版本、依赖等元数据，与 `lsmod` 互补使用。

## 统计已加载模块数量
```bash
lsmod | wc -l
```
```
87
```
> 共加载 87 个内核模块（含标题行则实际 86 个），用于快速评估系统模块规模。
