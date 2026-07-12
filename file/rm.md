# rm

## 删除单个文件
```bash
rm unwanted.txt
```
```
```
> 无输出即成功，文件被永久删除，不经过回收站。

## 交互式删除
```bash
rm -i *.log
```
```
rm: remove regular file 'access.log'? y
rm: remove regular file 'error.log'? n
```
> `-i` 每个文件删除前提示确认，避免误删。

## 强制递归删除目录
```bash
rm -rf /tmp/build/
```
```
```
> `-rf` 递归删除目录及其所有内容，不提示确认——极度危险。

## 删除并显示详情
```bash
rm -v *.tmp
```
```
removed 'cache.tmp'
removed 'session.tmp'
```
> `-v` 逐条显示每个被删除的文件。

## 强制删除不存在的文件也不报错
```bash
rm -f missing.txt
```
```
```
> `-f` 忽略不存在的文件，不报错，适合脚本中使用。

## 删除空目录
```bash
rm -d empty_folder
```
```
```
> `-d` 只删除空目录，相当于 `rmdir`。
