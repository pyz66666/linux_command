# systemctl

## 启动服务并设置开机自启
```bash
sudo systemctl start nginx && sudo systemctl enable nginx
```
```
Created symlink /etc/systemd/system/multi-user.target.wants/nginx.service → /lib/systemd/system/nginx.service.
```
> `start` 立即启动服务，`enable` 创建符号链接实现开机自启。

## 查看服务状态
```bash
systemctl status nginx
```
```
● nginx.service - A high performance web server
     Loaded: loaded (/lib/systemd/system/nginx.service; enabled; preset: enabled)
     Active: active (running) since Sun 2025-07-12 08:00:00 CST; 2h 30min ago
   Main PID: 1234 (nginx)
      Tasks: 5 (limit: 19000)
     Memory: 15.2M
        CPU: 345ms
     CGroup: /system.slice/nginx.service
             ├─1234 nginx: master process /usr/sbin/nginx
             ├─1235 nginx: worker process
             ├─1236 nginx: worker process
```
> 绿色 ● 表示正常运行，显示运行时长、PID、内存占用和进程树。

## 重启服务
```bash
sudo systemctl restart sshd
```
```
```
> `restart` 先停止再启动服务，服务会有短暂中断。

## 重载配置（不中断服务）
```bash
sudo systemctl reload nginx
```
```
```
> `reload` 只重新加载配置文件，不重启进程，服务无中断。

## 停止服务
```bash
sudo systemctl stop mysql
```
```
```
> 立即停止服务，但不会阻止下次开机自启。

## 取消开机自启
```bash
sudo systemctl disable mysql
```
```
Removed /etc/systemd/system/multi-user.target.wants/mysql.service.
```
> `disable` 移除开机自启符号链接，但当前运行不受影响。

## 检查服务是否运行
```bash
systemctl is-active nginx
```
```
active
```
> 返回 `active` 或 `inactive`，适合脚本中判断服务状态。

## 重载 systemd 配置
```bash
sudo systemctl daemon-reload
```
```
```
> 修改了 `.service` 文件后必须执行，让 systemd 重新读取配置。
