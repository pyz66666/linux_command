# zip / unzip

## 递归压缩目录
```bash
zip -r project.zip ./project/
```
```
  adding: project/ (stored 0%)
  adding: project/main.py (deflated 63%)
  adding: project/utils.py (deflated 58%)
  adding: project/config.yaml (deflated 45%)
  adding: project/static/ (stored 0%)
```
> `-r` 递归包含子目录，`deflated` 后的百分比表示压缩比例。

## 解压到指定目录
```bash
unzip archive.zip -d /tmp/extracted/
```
```
Archive:  archive.zip
  inflating: /tmp/extracted/main.py
  inflating: /tmp/extracted/utils.py
  inflating: /tmp/extracted/config.yaml
```
> `-d` 指定解压目标目录，目录不存在会自动创建。

## 不解压只查看内容
```bash
unzip -l backup.zip
```
```
Archive:  backup.zip
  Length      Date    Time    Name
---------  ---------- -----   ----
        0  2025-07-12 10:30   src/
     2048  2025-07-12 10:25   src/main.py
     1536  2025-07-12 10:26   src/utils.py
---------                     -------
     3584                     3 files
```
> `-l` 列出压缩包内容，包括文件大小、日期和总计。

## 加密压缩
```bash
zip -e secret.zip private.txt
```
```
Enter password:
Verify password:
  adding: private.txt (deflated 42%)
```
> `-e` 加密压缩，需输入两次密码确认。

## 压缩时排除特定文件
```bash
zip -r src.zip ./src/ -x "*.log" "*.pyc"
```
```
  adding: src/main.py (deflated 63%)
  adding: src/utils.py (deflated 58%)
  adding: src/config.yaml (deflated 45%)
```
> `-x` 排除匹配的文件，`.log` 和 `.pyc` 文件被跳过。
