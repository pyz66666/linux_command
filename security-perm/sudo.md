# sudo

## 查看当前用户 sudo 权限
```bash
sudo -l
```
```
Matching Defaults entries for user on my-server:
    env_reset, mail_badpass, secure_path=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

User user may run the following commands on my-server:
    (ALL : ALL) ALL
    (root) NOPASSWD: /usr/bin/systemctl restart nginx
```
> `(ALL : ALL) ALL` 表示拥有完整 root 权限，`NOPASSWD` 表示重启 nginx 无需密码。

## 以其他用户身份执行命令
```bash
sudo -u www-data whoami
```
```
www-data
```
> `-u` 以 www-data 身份运行 whoami，用于调试 Web 应用权限问题。

## 以 root 登录 shell 操作
```bash
sudo -i
```
```
root@my-server:~#
```
> `-i` 模拟 root 登录，加载 `/root/.bashrc` 等环境，比 `sudo su` 更规范且无需知道 root 密码。

## 执行单个特权命令
```bash
sudo systemctl restart nginx
```
> 最常用模式：以 root 身份执行单个命令，输入当前用户密码（非 root 密码）。

## 刷新 sudo 认证时间戳
```bash
sudo -v
```
> 延长 sudo 免密有效期（默认 15 分钟），之后执行 sudo 命令无需再次输入密码。

## 使 sudo 认证立即失效
```bash
sudo -k
```
> 下次执行 sudo 必须重新输入密码，用于离开终端时的安全保护。
