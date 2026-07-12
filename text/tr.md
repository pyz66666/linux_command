# tr

## 大小写转换
```bash
echo "Hello World" | tr '[:upper:]' '[:lower:]'
```
```
hello world
```
> `[:upper:]` 匹配所有大写字母，逐一替换为对应的小写字母。

## 替换分隔符
```bash
echo "A,B,C" | tr ',' '\n'
```
```
A
B
C
```
> 将逗号替换为换行符，每个值单独一行。

## 删除换行符（合并为一行）
```bash
cat file.txt | tr -d '\n'
```
```
line1 line2 line3 line4
```
> `-d` 删除所有换行符，多行合并为一行。

## 压缩连续空格
```bash
echo "hello    world    !" | tr -s ' '
```
```
hello world !
```
> `-s` 将连续多个空格压缩为单个空格。

## 删除 Windows 换行符
```bash
tr -d '\r' < dos.txt > unix.txt
```
```
```
> 删除回车符 `\r`，将 CRLF 换行转为 LF。

## 删除所有数字
```bash
echo "abc123def456" | tr -d '0-9'
```
```
abcdef
```
> 删除 0-9 所有数字字符，只保留字母。

## 字符集补集替换
```bash
echo "abc123!@#" | tr -c 'a-zA-Z0-9' '_'
```
```
abc123___
```
> `-c` 取补集，将非字母数字的字符替换为下划线 `_`。
