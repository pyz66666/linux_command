# mv

## 重命名文件
```bash
mv old_name.txt new_name.txt
```
```
```
> 无输出即成功，文件在原地改名，inode 不变。

## 移动文件到目录
```bash
mv file1.log file2.log /archive/logs/
```
```
```
> 最后一个参数是目标目录，前面所有文件被移入该目录。

## 移动并显示详情
```bash
mv -v *.csv /data/reports/
```
```
renamed 'sales.csv' -> '/data/reports/sales.csv'
renamed 'users.csv' -> '/data/reports/users.csv'
```
> `-v` 逐条显示移动操作记录。

## 交互式移动（覆盖前确认）
```bash
mv -i config.ini /etc/app/
```
```
mv: overwrite '/etc/app/config.ini'? n
```
> `-i` 在覆盖已存在文件前提示确认，输入 `n` 取消。

## 不覆盖已存在的文件
```bash
mv -n *.log /archive/
```
```
```
> `-n` 跳过目标位置已存在的同名文件，不会覆盖。

## 只移动较新的文件
```bash
mv -u build/* /deploy/
```
```
```
> `-u` 仅当源比目标新或目标不存在时才移动。
