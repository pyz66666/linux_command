# jobs / bg / fg

## 查看当前 shell 的作业列表
```bash
jobs -l
```
```
[1]  12345 Stopped (tty input)    vim notes.txt
[2] - 12346 Running                 python server.py &
[3] + 12350 Stopped (SIGTSTP)      tail -f /var/log/syslog
```
> `+` 标记当前作业，`-` 标记前一个，`Stopped` 表示被 Ctrl+Z 暂停。

## 后台运行命令
```bash
python server.py &
```
```
[1] 12346
```
> `&` 在后台启动进程，不阻塞终端，立即返回作业编号和 PID。

## 用 Ctrl+Z 暂停前台进程
```bash
tail -f /var/log/syslog
^Z
[2]+  Stopped                 tail -f /var/log/syslog
```
> Ctrl+Z 发送 `SIGTSTP` 信号暂停正在运行的前台进程。

## 将后台暂停作业调到前台
```bash
fg %1
```
```
# vim notes.txt 恢复到前台，可以继续编辑
```
> `%1` 引用作业编号 1，vim 恢复前台运行。

## 将暂停作业放到后台继续运行
```bash
bg %3
```
```
[3]+ tail -f /var/log/syslog &
```
> `%3` 将暂停的 tail 命令放到后台继续执行。

## 按名称引用作业
```bash
fg %vim
```
```
# 恢复 vim 到前台
```
> `%vim` 按命令行前缀匹配，快速切换常用作业。
