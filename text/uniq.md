# uniq

## 去重（相邻行）
```bash
sort logins.txt | uniq
```
```
alice
bob
carol
dave
```
> 先 `sort` 排序让相同行相邻，`uniq` 去除重复行。

## 统计每行出现次数
```bash
sort access.log | uniq -c | sort -rn
```
```
    148 192.168.1.100
     32 192.168.1.101
     15 10.0.0.5
      5 172.16.0.1
      1 192.168.1.200
```
> `-c` 在每行前显示出现次数，再 `sort -rn` 按次数降序排列。

## 只显示重复行
```bash
sort data.txt | uniq -d
```
```
192.168.1.100
192.168.1.101
```
> `-d` 只输出出现多次的行，出现 1 次的被排除。

## 只显示唯一行
```bash
sort data.txt | uniq -u
```
```
10.0.0.5
192.168.1.200
```
> `-u` 只输出恰好出现 1 次的行。

## 忽略前 N 个字段去重
```bash
sort access.log | uniq -f 1 -c
```
```
    5 2025-07-12 192.168.1.100
    3 2025-07-11 10.0.0.5
```
> `-f 1` 跳过第一个字段再比较，按 IP 而非日期去重统计。

## 忽略大小写去重
```bash
sort items.txt | uniq -i
```
```
apple
Banana
cherry
```
> `-i` 忽略大小写，`Banana` 和 `banana` 被视为相同。
