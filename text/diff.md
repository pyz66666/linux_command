# diff

## 对比两个文件差异
```bash
diff -u old.conf new.conf
```
```
--- old.conf    2025-07-10 08:00:00.000000000 +0800
+++ new.conf    2025-07-12 10:30:00.000000000 +0800
@@ -3,7 +3,8 @@
 server {
     listen       80;
+    server_name  example.com;
     location / {
-        root   /var/www/old;
+        root   /var/www/new;
     }
```
> `-u` 统一格式，`+` 表示新增行，`-` 表示删除行，最易阅读。

## 只检查文件是否相同
```bash
diff -q a.txt b.txt
```
```
Files a.txt and b.txt differ
```
> `-q` 只报告是否不同，不显示具体差异内容。

## 递归比较两个目录
```bash
diff -ur dir_old/ dir_new/
```
```
diff -ur dir_old/config.yaml dir_new/config.yaml
--- dir_old/config.yaml  2025-07-10 08:00:00
+++ dir_new/config.yaml  2025-07-12 10:30:00
@@ -1,5 +1,6 @@
 server:
   port: 8080
+  debug: false
   log_level: info
Only in dir_new/: new_feature.py
```
> `-r` 递归比较所有子目录和文件，`Only in` 表示只在某一方存在的文件。

## 左右并列显示
```bash
diff -y old.txt new.txt
```
```
hello world                     hello world
old content                  |  new content
same line                       same line
deleted line                 <
                              > added line
```
> `-y` 左右分栏，`|` 表示不同，`<` 只在左边，`>` 只在右边。

## 忽略空白差异
```bash
diff -uw old.py new.py
```
```
--- old.py 2025-07-10 08:00:00
+++ new.py 2025-07-12 10:30:00
@@ -5,6 +5,3 @@
 def main():
-    pass
+    print("Hello")
```
> `-w` 忽略空格和制表符差异，只关注实质内容变化。
