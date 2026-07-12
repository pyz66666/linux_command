# passwd

## 修改自己的密码
```bash
passwd
```
```
Changing password for user.
Current password:
New password:
Retype new password:
passwd: password updated successfully
```
> 普通用户只能改自己的密码，需要输入当前密码验证。

## 查看用户密码状态
```bash
sudo passwd -S alice
```
```
alice P 07/12/2026 0 90 7 30
```
> P=密码已设置，最后修改 2026-07-12，最短 0 天可改，最长 90 天过期，过期前 7 天警告，过期后 30 天仍可登录。

## 强制用户下次登录修改密码
```bash
sudo passwd -e alice
```
```
passwd: password expiry information changed.
```
> `-e` 立即让密码过期，alice 下次登录被要求修改密码，适合初始密码分发场景。

## 锁定和解锁用户
```bash
sudo passwd -l alice
sudo passwd -S alice
```
```
alice L 07/12/2026 0 90 7 30
```
```
sudo passwd -u alice
```
> `-l` 在 `/etc/shadow` 密码前加 `!` 锁定（无法密码登录但 SSH key 仍可用），`-u` 解锁。

## 删除用户密码
```bash
sudo passwd -d alice
```
```
passwd: password expiry information changed.
```
> `-d` 删除密码后 alice 可无密码登录，极度危险，仅用于特定场景（如 kiosk 模式）。

## 查看所有用户密码状态
```bash
sudo passwd -S -a
```
```
root P 06/01/2026 0 99999 7 -1
alice P 07/12/2026 0 90 7 30
bob L 05/15/2026 0 90 7 30
www-data L 01/01/2020 -1 -1 -1 -1
```
> `-a` 显示所有用户状态，www-data 等系统账户通常是 L（锁定）且无过期策略。
