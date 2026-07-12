# ssh-keygen

## 生成 Ed25519 密钥对
```bash
ssh-keygen -t ed25519 -C "user@example.com" -f ~/.ssh/id_ed25519
```
```
Generating public/private ed25519 key pair.
Enter passphrase (empty for no passphrase):
Your identification has been saved in /home/user/.ssh/id_ed25519
Your public key has been saved in /home/user/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:AbC123XyZ/abcdefghijklmnopqrstuvwxyz1234 user@example.com
```
> 私钥 `id_ed25519`（权限 600 不能泄露），公钥 `id_ed25519.pub`（放目标服务器 authorized_keys），推荐 Ed25519 算法。

## 查看密钥指纹
```bash
ssh-keygen -lf ~/.ssh/id_ed25519.pub
```
```
256 SHA256:AbC123XyZ/abcdefghijklmnopqrstuvwxyz1234 user@example.com (ED25519)
```
> `-l` 显示指纹用于核对密钥身份，256 表示 256 位 ED25519 密钥。

## 从 known_hosts 删除过期主机
```bash
ssh-keygen -R old-server.example.com
```
```
# Host old-server.example.com found: line 42
/home/user/.ssh/known_hosts updated.
```
> 服务器重装后 host key 变化导致 SSH 警告时，用 `-R` 删除旧记录即可重新连接。

## 修改已有密钥的密码短语
```bash
ssh-keygen -p -f ~/.ssh/id_ed25519
```
```
Enter old passphrase:
Enter new passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved with the new passphrase.
```
> `-p` 修改私钥的保护密码，不改变密钥本身。

## 批量部署公钥
```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@remote-server
```
```
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s)
Number of key(s) added: 1
```
> `ssh-copy-id` 自动将公钥追加到目标服务器的 `~/.ssh/authorized_keys`，免密登录配置一步到位。
