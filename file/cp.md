# cp

## 复制单个文件
```bash
cp config.yaml config.yaml.bak
```
```
```
> 无输出即成功，在当前目录生成备份文件 `config.yaml.bak`。

## 递归复制目录（保留属性）
```bash
cp -a /data/project /backup/project_2025
```
```
```
> `-a` 归档模式：递归复制并保留权限、时间戳等所有属性。

## 复制并显示进度
```bash
cp -v *.txt /tmp/texts/
```
```
'readme.txt' -> '/tmp/texts/readme.txt'
'notes.txt' -> '/tmp/texts/notes.txt'
'todo.txt' -> '/tmp/texts/todo.txt'
```
> `-v` 逐条显示每个被复制的文件及其目标路径。

## 交互式复制（覆盖前确认）
```bash
cp -i nginx.conf /etc/nginx/nginx.conf
```
```
cp: overwrite '/etc/nginx/nginx.conf'? y
```
> `-i` 在覆盖已存在文件前提示确认，防止误覆盖。

## 只复制较新的文件
```bash
cp -u *.py /backup/src/
```
```
```
> `-u` 仅当源比目标新或目标不存在时才复制，避免重复复制。

## 批量复制到目录
```bash
cp *.jpg *.png /images/
```
```
```
> 支持多个源文件以空格分隔，最后一个参数必须是目标目录。
