# nice / renice

## 以较低优先级启动进程
```bash
nice -n 19 tar -czf backup.tar.gz /large/dir/
```
```
```
> `-n 19` 最低优先级，备份任务不会影响交互式操作响应。

## 查看进程的 nice 值
```bash
ps -o pid,ni,comm -p 67890
```
```
  PID  NI COMMAND
67890  19 tar
```
> `NI` 列显示 nice 值为 19，数字越大优先级越低。

## 降低正在运行进程的优先级
```bash
renice -n 10 -p 12345
```
```
12345 (process ID) old priority 0, new priority 10
```
> 将 PID 12345 的优先级从 0 降到 10，释放 CPU 给其他进程。

## 提高优先级需要 root
```bash
renice -n -5 -p 12345
```
```
renice: failed to set priority for 12345: Permission denied
```
> 普通用户只能上调 nice 值（降低优先级），负值需要 root 权限。

## 按用户调整所有进程优先级
```bash
sudo renice -n 5 -u www-data
```
```
1000 (user ID) old priority 0, new priority 5
```
> `-u` 调整指定用户所有进程的优先级，需 root 权限。

## 查看默认优先级对比
```bash
ps -eo pid,ni,comm | grep -E "tar|python"
```
```
67890  19 tar
12345   0 python
```
> 默认启动 nice 值为 0，`nice -n 19` 的后台任务优先级明显降低。
