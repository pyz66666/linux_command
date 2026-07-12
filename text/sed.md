# sed

## 替换每行第一个匹配
```bash
sed 's/old/new/' file.txt
```
```
hello new world, old friend
```
> `s/old/new/` 只替换每行第一个匹配到的 `old`，第二个 `old` 保留原样。

## 全局替换
```bash
sed 's/old/new/g' file.txt
```
```
hello new world, new friend
```
> `g` 标志替换每行的所有匹配，两个 `old` 都被替换。

## 直接修改文件
```bash
sed -i 's/DEBUG/INFO/g' config.yaml
```
```
```
> `-i` 直接修改原文件不输出到屏幕，全局替换所有 `DEBUG` 为 `INFO`。

## 修改前备份原文件
```bash
sed -i.bak 's/localhost/192.168.1.100/' nginx.conf
```
```
```
> `-i.bak` 修改前生成 `nginx.conf.bak` 备份文件。

## 删除匹配行
```bash
sed '/^#/d' nginx.conf | head -3
```
```
server {
    listen 80;
    server_name example.com;
```
> `/^#/d` 删除以 `#` 开头的注释行，输出去掉注释后的配置。

## 删除空行
```bash
sed '/^[[:space:]]*$/d' file.txt
```
```
line 1
line 2
line 3
```
> 删除所有空行和只包含空格/制表符的行。

## 打印指定行范围
```bash
sed -n '5,10p' app.log
```
```
2025-07-12 08:30:05 DEBUG Request received
2025-07-12 08:30:06 INFO Processing
2025-07-12 08:30:07 DEBUG Validating input
2025-07-12 08:30:08 INFO Sending response
2025-07-12 08:30:09 DEBUG Cleaning up
2025-07-12 08:30:10 INFO Request complete
```
> `-n` 禁止默认输出，`5,10p` 只打印第 5 到 10 行。
