# ls

## 列出当前目录文件
```bash
ls
```
```
app.py  config  README.md  run.sh
```
> 默认不显示隐藏文件，按字母顺序排列。

## 长格式显示详细信息
```bash
ls -l
```
```
total 12K
drwxr-xr-x 2 alice devs 4.0K Jun 10 14:22 config
-rw-r--r-- 1 alice devs  850 Jun 12 09:15 app.py
-rw-r--r-- 1 alice devs 1.2K Jun 12 09:30 README.md
-rwxr-xr-x 1 alice devs  300 Jun 11 18:00 run.sh
```
> `-l` 显示权限、大小、时间等详细信息，首字节 `d` 表示目录。

## 显示所有文件包括隐藏文件
```bash
ls -la
```
```
total 20K
drwxr-xr-x 3 alice devs 4.0K Jul 12 10:30 .
drwxr-xr-x 5 alice devs 4.0K Jul 12 09:00 ..
-rw-r--r-- 1 alice devs  850 Jun 12 09:15 app.py
drwxr-xr-x 2 alice devs 4.0K Jun 10 14:22 config
-rw-r--r-- 1 alice devs   42 Jul 12 10:30 .env
-rw-r--r-- 1 alice devs 1.2K Jun 12 09:30 README.md
-rwxr-xr-x 1 alice devs  300 Jun 11 18:00 run.sh
```
> `-a` 显示 `.` 开头的隐藏文件，包括 `.env` 和目录自身 `.`、`..`。

## 按修改时间排序
```bash
ls -lt
```
```
total 12K
-rw-r--r-- 1 alice devs   42 Jul 12 10:30 .env
-rw-r--r-- 1 alice devs  850 Jun 12 09:15 app.py
-rw-r--r-- 1 alice devs 1.2K Jun 12 09:30 README.md
-rw-r--r-- 1 alice devs  300 Jun 11 18:00 run.sh
drwxr-xr-x 2 alice devs 4.0K Jun 10 14:22 config
```
> `-t` 按修改时间从新到旧排列，最新的文件在最前。

## 人类可读大小 + 按时间排序
```bash
ls -lhS
```
```
total 12K
drwxr-xr-x 2 alice devs 4.0K Jun 10 14:22 config
-rw-r--r-- 1 alice devs 1.2K Jun 12 09:30 README.md
-rw-r--r-- 1 alice devs  850 Jun 12 09:15 app.py
-rwxr-xr-x 1 alice devs  300 Jun 11 18:00 run.sh
```
> `-h` 将大小转为 K/M/G 可读格式，`-S` 按文件大小降序排列。

## 只列出目录
```bash
ls -d */
```
```
config/  tests/  docs/
```
> `-d */` 只显示当前目录下的子目录，不显示普通文件。

## 递归列出所有文件
```bash
ls -R
```
```
.:
app.py  config  README.md  run.sh

./config:
database.yaml  logging.yaml

./tests:
test_main.py
```
> `-R` 递归进入每个子目录并显示其内容。
