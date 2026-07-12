# wc

## 统计文件行数
```bash
wc -l access.log
```
```
1500 access.log
```
> `-l` 只显示行数和文件名，`access.log` 共 1500 行。

## 统计行数、单词数、字节数
```bash
wc access.log
```
```
   1500   12300  258400 access.log
```
> 三列分别是：行数、单词数、字节数（文件大小）。

## 统计多个文件（含汇总）
```bash
wc -l *.py
```
```
    85 main.py
   120 utils.py
    45 config.py
   250 total
```
> 每个文件一行，最后一行为 `total` 汇总。

## 管道输入统计（无文件名）
```bash
grep "ERROR" app.log | wc -l
```
```
23
```
> 管道输入时只输出数字，不显示文件名，适合脚本赋值。

## 统计字符数（区分字节和字符）
```bash
wc -m chinese.txt
```
```
120 chinese.txt
```
> `-m` 统计字符数，对中文等 UTF-8 多字节字符更准确。

## 显示最长行长度
```bash
wc -L data.csv
```
```
245 data.csv
```
> `-L` 显示文件中最长一行的字符数，适合检查 CSV 行宽。
