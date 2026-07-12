# sort

## 字典序排列
```bash
sort names.txt
```
```
Alice
Bob
alice
bob
```
> 默认字典序，大写字母排在小写之前（基于 ASCII）。

## 数值排序
```bash
sort -n sizes.txt
```
```
2
10
50
100
```
> `-n` 按数值排序，`10` 排在 `2` 后面而不是前面。

## 降序排列
```bash
sort -rn scores.txt
```
```
alice 95
carol 88
dave 72
bob 72
```
> `-r` 反转顺序，从高到低排列。

## 按指定列排序
```bash
sort -k2 -n data.txt
```
```
bob 72
dave 72
carol 88
alice 95
```
> `-k2` 按第二列排序，`-n` 数值排序。

## 按文件大小排序
```bash
du -h | sort -hr | head -5
```
```
12G     ./videos
3.5G    ./music
850M    ./documents
120M    ./photos
45M     ./scripts
```
> `-h` 识别人类可读大小单位（K/M/G），`-r` 降序，最大文件在前。

## 去重排序
```bash
sort -u items.txt
```
```
apple
banana
cherry
```
> `-u` 排序同时去重，等价于 `sort | uniq`。

## 按逗号分隔字段排序
```bash
sort -t',' -k2 data.csv
```
```
李四,运维部,5年
张三,研发部,3年
王五,测试部,2年
```
> `-t','` 指定逗号分隔符，`-k2` 按第二列（部门）排序。
