# gzip / gunzip

## 压缩文件
```bash
gzip large.log
```
```
```
> 原文件被替换为 `large.log.gz`，压缩比通常 50%~70%。

## 解压文件
```bash
gunzip large.log.gz
```
```
```
> 恢复原始文件 `large.log`，`.gz` 文件被删除。

## 压缩并显示压缩比
```bash
gzip -v data.txt
```
```
data.txt:    57.3% -- replaced with data.txt.gz
```
> `57.3%` 表示压缩后大小为原来的 57.3%，缩小了约 42.7%。

## 压缩但保留原文件
```bash
gzip -k access.log
```
```
```
> `-k` 保留原始文件，同时生成 `access.log.gz`。

## 最高压缩率
```bash
gzip -9v backup.sql
```
```
backup.sql:    23.1% -- replaced with backup.sql.gz
```
> `-9` 最高压缩级别，文本文件压缩效果尤其显著。

## 查看压缩文件内容
```bash
zcat file.gz | head -5
```
```
line 1 content
line 2 content
line 3 content
line 4 content
line 5 content
```
> `zcat` 不解压直接查看 `.gz` 文件内容。

## 测试压缩文件完整性
```bash
gzip -t archive.gz
```
```
```
> `-t` 无输出表示文件完整未损坏，有错误会报告。
