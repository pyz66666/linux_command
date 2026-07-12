# modprobe

## 查看模块依赖关系
```bash
modprobe --show-depends iwlwifi
```
```
insmod /lib/modules/6.5.0-14-generic/kernel/net/wireless/cfg80211.ko
insmod /lib/modules/6.5.0-14-generic/kernel/net/mac80211/mac80211.ko
insmod /lib/modules/6.5.0-14-generic/kernel/drivers/net/wireless/intel/iwlwifi/iwlwifi.ko
```
> iwlwifi 依赖 cfg80211 和 mac80211，modprobe 会自动按依赖顺序加载。

## 加载模块并查看详细过程
```bash
sudo modprobe -v vboxdrv
```
```
insmod /lib/modules/6.5.0-14-generic/misc/vboxdrv.ko
```
> `-v` 显示加载过程，vboxdrv（VirtualBox 驱动）无额外依赖直接加载。

## 卸载模块
```bash
sudo modprobe -r vboxdrv
```
> 无输出即成功，`-r` 会同时卸载不被其他模块依赖的依赖模块。

## 加载模块并传递参数
```bash
sudo modprobe iwlwifi power_save=0 11n_disable=1
```
> `power_save=0` 禁用 WiFi 省电模式，`11n_disable=1` 禁用 802.11n，用于解决兼容性问题。

## 查看模块别名和配置
```bash
modprobe -c | grep -i nvidia | head -5
```
```
alias pci:v000010DEd*sv*sd*bc03sc00i00* nvidia
alias pci:v000010DEd*sv*sd*bc03sc02i00* nvidia
alias symbol:nvidia* nvidia
blacklist nvidiafb
```
> `-c` 显示完整模块配置，包括别名（自动匹配硬件）和黑名单规则。

## 演习模式
```bash
modprobe -n -v iwlwifi
```
```
insmod /lib/modules/6.5.0-14-generic/kernel/net/wireless/cfg80211.ko
insmod /lib/modules/6.5.0-14-generic/kernel/net/mac80211/mac80211.ko
insmod /lib/modules/6.5.0-14-generic/kernel/drivers/net/wireless/intel/iwlwifi/iwlwifi.ko
```
> `-n` dry-run 模式，显示将要执行的操作但不实际加载模块。
