# touch

## 创建空文件
```bash
touch newfile.txt
```
```
```
> 无输出即成功，文件大小为 0 字节；如果文件已存在则只更新时间为当前时刻。

## 批量创建多个文件
```bash
touch file{1..5}.txt
```
```
```
> 花括号展开为 `file1.txt` 到 `file5.txt`，一次性创建 5 个空文件。

## 验证文件已创建
```bash
ls -lh newfile.txt
```
```
-rw-r--r-- 1 alice devs 0 Jul 12 10:30 newfile.txt
```
> 大小为 `0`，时间戳为当前时刻，已成功创建。

## 将时间戳设为指定日期
```bash
touch -d "2025-06-01 08:30:00" deploy.log
```
```
```
> `-d` 将文件的修改时间设置为指定日期，不影响文件内容。

## 验证时间戳已修改
```bash
ls -l deploy.log
```
```
-rw-r--r-- 1 alice devs 1024 Jun  1  2025 deploy.log
```
> 修改时间变为 `Jun 1 2025`，即使文件实际是今天创建的。

## 以参考文件的时间设置
```bash
touch -r reference.txt target.txt
```
```
```
> `-r` 让 `target.txt` 的时间戳与 `reference.txt` 完全一致。
