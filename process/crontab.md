# crontab

## 列出当前用户的定时任务
```bash
crontab -l
```
```
# 每天凌晨 2 点备份数据库
0 2 * * * /usr/local/bin/backup_db.sh >> /var/log/backup.log 2>&1

# 每小时的第 5 分钟清理临时文件
5 * * * * find /tmp -type f -mtime +7 -delete

# 每周日凌晨 3 点重启服务
0 3 * * 0 systemctl restart myapp
```
> 每行一个任务：`分 时 日 月 周 命令`，`*` 表示"每"。

## 编辑 crontab
```bash
crontab -e
```
```
# 进入默认文本编辑器，编辑后保存退出即生效
```
> `-e` 打开编辑器编辑定时任务，保存后自动安装。

## 删除所有定时任务
```bash
crontab -r
```
```
```
> 删除当前用户所有 crontab 任务，不可恢复。

## 删除前确认
```bash
crontab -ri
```
```
crontab: really delete alice's crontab? n
```
> `-i` 删除前提示确认，输入 `n` 取消。

## 查看其他用户的 crontab
```bash
sudo crontab -u www-data -l
```
```
*/10 * * * * /usr/bin/php /var/www/html/cron.php
```
> `-u` 需要 root 权限，查看指定用户的定时任务。

## Crontab 时间格式速查
```bash
# ┌─ 分钟 (0-59)
# │ ┌─ 小时 (0-23)
# │ │ ┌─ 日 (1-31)
# │ │ │ ┌─ 月 (1-12)
# │ │ │ │ ┌─ 星期 (0-7, 0/7=周日)
# │ │ │ │ │
# * * * * * 命令
```
```
# 每分钟执行：  * * * * *
# 每天 00:00：  0 0 * * *
# 每周一 3:00： 0 3 * * 1
# 每月 1 号：   0 0 1 * *
# 每 10 分钟：  */10 * * * *
```
> `*/N` 表示每 N 个单位执行一次，`*/10` 即每 10 分钟。
