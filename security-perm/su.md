# su

## 切换到 root
```bash
su -
```
```
Password:
root@my-server:~#
```
> `su -` 加载 root 完整环境（工作目录切到 /root、加载 .bashrc），需要输入 root 密码。

## 以其他用户身份执行单条命令
```bash
su - alice -c "whoami && pwd"
```
```
alice
/home/alice
```
> `-c` 执行单条命令后立即退出，不进入交互 shell，需要 alice 的密码（除非 root 执行）。

## 切换到 www-data 排查权限
```bash
sudo su - www-data -s /bin/bash
whoami
touch /var/www/html/test.txt
```
```
www-data
touch: cannot touch '/var/www/html/test.txt': Permission denied
```
> `sudo su - www-data` 以 root 运行 su（无需 www-data 密码），touch 失败说明目录所有者不是 www-data。

## 切换到普通用户
```bash
su alice
whoami
pwd
```
```
alice
/home/original_user
```
> 不加 `-` 的 su 保留当前工作目录和环境变量，可能导致 PATH 异常。

## 用 sudo 替代 su 获取 root shell
```bash
sudo -i
```
```
root@my-server:~#
```
> `sudo -i` 更推荐：使用自己的密码、有审计日志、无需知道 root 密码。
