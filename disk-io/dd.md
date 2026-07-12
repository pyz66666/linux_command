# dd

## 测试磁盘写入速度
```bash
dd if=/dev/zero of=./speedtest bs=1M count=1024 oflag=direct status=progress
```
```
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 3.542 s, 303 MB/s
1024+0 records in
1024+0 records out
```
> `oflag=direct` 绕过页缓存测真实磁盘性能，303 MB/s 是此盘的顺序写入速率。

## 创建指定大小的空白文件
```bash
dd if=/dev/zero of=testfile bs=1M count=1024 status=progress
```
```
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 0.812 s, 1.3 GB/s
1024+0 records in
1024+0 records out
```
> 从 `/dev/zero` 读取零字节创建 1GB 空文件，可用于交换文件或占位测试。

## 克隆整个磁盘
```bash
dd if=/dev/sda of=/dev/sdb bs=4M status=progress
```
```
53687091200 bytes (54 GB, 50 GiB) copied, 345 s, 155 MB/s
12800+0 records in
12800+0 records out
```
> `if` 是源盘 `of` 是目标盘，务必确认不能写反，否则数据不可恢复。

## 擦除磁盘数据
```bash
dd if=/dev/zero of=/dev/sdb bs=1M status=progress
```
```
214748364800 bytes (215 GB, 200 GiB) copied, 720 s, 298 MB/s
204800+0 records in
204800+0 records out
```
> 写入全零覆盖整个磁盘，用于销毁数据或清除分区表后重新初始化。

## 抢救损坏磁盘数据
```bash
dd if=/dev/sdb of=rescue.img bs=512 conv=noerror,sync status=progress
```
```
53687091200 bytes (54 GB, 50 GiB) copied, 4230 s, 12.7 MB/s
104857600+2 records in
104857600+0 records out
```
> `conv=noerror,sync` 遇到读取错误跳过并用零填充，尽可能多地恢复数据；`+2` 表示有 2 个不完整的坏块。
