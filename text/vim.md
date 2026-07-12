# vim

## 打开或创建文件
```bash
vim config.yaml
```
```
~
~
"config.yaml" [New File]
```
> 波浪线 `~` 表示空行，`[New File]` 表示正在创建新文件。

## 打开文件并跳到指定行
```bash
vim +100 app.log
```
```
...
2025-07-12 08:05:00 INFO Row 100
2025-07-12 08:05:01 WARN Row 101
...
```
> `+100` 打开文件后光标自动定位到第 100 行。

## 打开文件并跳到首次匹配
```bash
vim +/ERROR app.log
```
```
2025-07-12 08:30:01 ERROR Database connection failed
2025-07-12 09:15:22 ERROR Timeout sending email
```
> `+/ERROR` 打开后光标跳到第一个 `ERROR` 匹配处。

## 左右分屏比较两个文件
```bash
vim -d old.conf new.conf
```
```
server {                |  server {
    listen 80;          |      listen 80;
    root /var/www/old;  |      root /var/www/new;
                        |      server_name example.com;
```
> `-d` diff 模式，左右分屏并高亮差异，方便做代码审查。

## 基本编辑操作
```bash
vim notes.txt
```
```
Hello World
~
~
-- INSERT --
```
> 按 `i` 进入插入模式开始编辑，按 `Esc` 回到普通模式，输入 `:wq` 保存退出。

## 只读模式打开
```bash
vim -R /etc/nginx/nginx.conf
```
```
user www-data;
worker_processes auto;
~
"nginx.conf" [readonly]
```
> `-R` 只读模式，防止意外修改系统配置文件。
