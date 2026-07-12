# nohup

## 后台运行并忽略终端关闭
```bash
nohup python train_model.py &
```
```
[1] 56789
nohup: ignoring input and appending output to 'nohup.out'
```
> `[1]` 是作业编号，`56789` 是 PID，输出默认写入当前目录的 `nohup.out`。

## 指定日志输出文件
```bash
nohup ./server --port=8080 > server.log 2>&1 &
```
```
[1] 56800
nohup: ignoring input and appending output to 'server.log'
```
> `> server.log 2>&1` 将 stdout 和 stderr 都重定向到指定日志文件。

## 查看 nohup 输出的日志
```bash
cat nohup.out
```
```
2025-07-12 10:30:00 Task started
2025-07-12 10:30:05 Processing batch 1/100...
2025-07-12 10:31:20 Task completed successfully
```
> 关闭终端后进程不中断，日志持续写入，可以随时查看进度。

## 启动后验证进程存在
```bash
nohup long_task.sh & pgrep long_task
```
```
[1] 57001
57001
```
> 启动后立即用 `pgrep` 确认进程是否成功运行。

## 完全脱离 shell
```bash
nohup python app.py > app.log 2>&1 & disown
```
```
[1] 58000
```
> `disown` 将作业从 shell 作业表中移除，即使退出当前 bash 也不会被杀（部分 shell 适用）。
