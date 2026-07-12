# cut

## 按分隔符提取字段
```bash
cut -d':' -f1,7 /etc/passwd
```
```
root:/bin/bash
daemon:/usr/sbin/nologin
alice:/bin/zsh
bob:/bin/bash
```
> `-d':'` 冒号分隔，`-f1,7` 提取第 1 和第 7 个字段（用户名和 shell）。

## 按字符位置提取
```bash
cut -c1-10 file.txt
```
```
2025-07-12
2025-07-13
2025-07-14
```
> `-c1-10` 提取每行第 1 到第 10 个字符。

## 提取 CSV 的指定列
```bash
cut -d',' -f1,3 data.csv
```
```
张三,研发部
李四,运维部
王五,测试部
```
> 逗号分隔，提取第 1 列（姓名）和第 3 列（部门）。

## 跳过无分隔符的行
```bash
cut -d',' -f1,2 -s mixed.txt
```
```
alice,30
bob,25
```
> `-s` 跳过不包含分隔符的行，只输出有逗号的 CSV 行。

## 修改输出分隔符
```bash
cut -d':' -f1,7 --output-delimiter=' | ' /etc/passwd
```
```
root | /bin/bash
alice | /bin/zsh
```
> `--output-delimiter` 将输出中的冒号替换为自定义分隔符。
