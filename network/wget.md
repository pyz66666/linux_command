# wget

## 下载单个文件
```bash
wget https://releases.example.com/app-3.2.1-linux-amd64.tar.gz
```
```
--2026-07-12 10:00:00--  https://releases.example.com/app-3.2.1-linux-amd64.tar.gz
Resolving releases.example.com... 93.184.216.34
Connecting to releases.example.com|93.184.216.34|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 52428800 (50M) [application/gzip]
Saving to: 'app-3.2.1-linux-amd64.tar.gz'

app-3.2.1-linux-amd64.tar.gz  100%[=====================>]  50.00M  12.5MB/s    in 4.0s

2026-07-12 10:00:04 (12.5 MB/s) - 'app-3.2.1-linux-amd64.tar.gz' saved [52428800/52428800]
```
> 进度条显示下载百分比、速度和耗时，文件名自动取自 URL 最后一段，完整性验证通过。

## 断点续传
```bash
wget -c https://example.com/large_dataset.iso
```
```
--2026-07-12 10:05:00--  https://example.com/large_dataset.iso
Resolving example.com... 93.184.216.34
Connecting to example.com|93.184.216.34|:443... connected.
HTTP request sent, awaiting response... 206 Partial Content
Length: 4294967296 (4.0G), 2147483648 (2.0G) remaining [application/octet-stream]
Saving to: 'large_dataset.iso'

large_dataset.iso            55%[++++++++++====>        ]   2.20G  10.0MB/s    eta 3m 30s
```
> `-c` 从中断点继续下载，服务器返回 `206 Partial Content` 确认支持续传，节省时间和带宽。

## 指定保存文件名
```bash
wget -O myapp.tar.gz https://example.com/releases/v2.0.tar.gz
```
```
--2026-07-12 10:10:00--  https://example.com/releases/v2.0.tar.gz
Saving to: 'myapp.tar.gz'

myapp.tar.gz                 100%[=====================>]  25.00M  8.3MB/s    in 3.0s
```
> `-O` 自定义保存文件名，当 URL 最后一段不含可读文件名时尤其必要。

## 限速下载
```bash
wget --limit-rate=1m https://example.com/file.iso
```
```
Saving to: 'file.iso'

file.iso                     12%[===>                   ]  480M  1.00MB/s    eta 58m 30s
```
> `--limit-rate=1m` 将下载速度限制在 1MB/s，避免占满带宽影响其他服务。

## 后台静默下载
```bash
wget -b -q https://example.com/backup.tar.gz
```
```
Continuing in background, pid 12345.
Output will be written to 'wget-log'.
```
> `-b` 后台运行，`-q` 静默模式，适合在脚本中不阻塞地下载大文件，进度写入 `wget-log`。
