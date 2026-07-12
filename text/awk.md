# awk

## 打印指定列
```bash
awk '{print $1, $3}' data.txt
```
```
alice 92
bob 88
carol 76
```
> 默认空白分隔，`$1` 是第一列，`$3` 是第三列，逗号分隔输出列。

## 按分隔符提取字段
```bash
awk -F',' '{print $1, $3}' data.csv
```
```
张三 研发部
李四 运维部
王五 测试部
```
> `-F','` 指定逗号为分隔符，适用于 CSV 文件。

## 条件筛选
```bash
awk '$3 > 90 {print $0}' scores.txt
```
```
alice 85 95
carol 88 92
```
> 只输出第三列（成绩）大于 90 的行，`$0` 表示整行。

## 计算和统计
```bash
awk '{sum += $2} END {print "Total:", sum, "Avg:", sum/NR}' scores.txt
```
```
Total: 255  Avg: 85
```
> `END` 块在所有行处理完后执行，`NR` 是总行数。

## 格式化输出
```bash
awk '{printf "%-10s %3d\n", $1, $2}' students.txt
```
```
alice        95
bob          72
carol        88
```
> `printf` 格式化输出，左对齐 10 字符宽，成绩占 3 字符右对齐。

## 结合正则过滤
```bash
awk '/ERROR/ {print $1, $2, $NF}' app.log
```
```
2025-07-12 08:30:01 failed
2025-07-12 09:15:22 email
```
> `/ERROR/` 只处理包含 ERROR 的行，`$NF` 是最后一列。
