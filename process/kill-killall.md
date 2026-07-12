# kill / killall

## 优雅终止进程（默认信号）
```bash
kill 12345
```
```
```
> 无输出即成功，默认发送 `SIGTERM (15)`，给进程清理资源的机会。

## 强制终止进程
```bash
kill -9 12346
```
```
```
> `-9` 发送 `SIGKILL`，内核直接终止进程，无法被应用捕获或忽略。

## 重载配置（不中断服务）
```bash
kill -HUP $(cat /var/run/nginx.pid)
```
```
```
> `-HUP` (1) 信号通知守护进程重新加载配置文件，服务不中断。

## 按名称终止所有匹配进程
```bash
killall python
```
```
```
> 终止所有名为 `python` 的进程，默认发送 `SIGTERM`。

## 强制终止指定名称的进程
```bash
killall -9 java
```
```
```
> `-9` 强制终止所有 Java 进程，慎用——会杀死不相关的 Java 程序。

## 终止指定用户的进程
```bash
killall -u www-data nginx
```
```
```
> `-u` 限定为指定用户，不会误杀其他用户的同名进程。

## 列出所有可用信号
```bash
kill -l
```
```
 1) SIGHUP       2) SIGINT       3) SIGQUIT      4) SIGILL
 5) SIGTRAP      6) SIGABRT      7) SIGBUS       8) SIGFPE
 9) SIGKILL     10) SIGUSR1     11) SIGSEGV     12) SIGUSR2
13) SIGPIPE     14) SIGALRM     15) SIGTERM
```
> 列出信号编号与名称对应关系，`15 (TERM)` 最常用，`9 (KILL)` 是最后手段。
