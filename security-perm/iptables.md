# iptables

## 列出所有规则
```bash
sudo iptables -L -n -v --line-numbers
```
```
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination
1      234  12345 ACCEPT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0            tcp dpt:22
2     1234 987654 ACCEPT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0            tcp dpt:80
3        0      0 DROP       tcp  --  *      *       192.168.1.200        0.0.0.0/0            tcp dpt:22
4    45678 3456K ACCEPT     all  --  *      *       0.0.0.0/0            0.0.0.0/0            state RELATED,ESTABLISHED
```
> 规则 #1 放行 SSH、#2 放行 HTTP、#3 封禁 192.168.1.200 访问 SSH、#4 放行已建立连接的回复包。

## 开放端口
```bash
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT
```
> `-A` 在 INPUT 链末尾追加规则，放行 TCP 443 端口（HTTPS）。

## 封禁特定 IP
```bash
sudo iptables -I INPUT -s 10.0.0.99 -j DROP
```
> `-I` 在链最前面插入规则，来自 10.0.0.99 的所有包直接丢弃。

## 删除规则
```bash
sudo iptables -D INPUT 3
```
> `-D` 删除 INPUT 链第 3 条规则，删除后需重新 `-L --line-numbers` 确认。

## 保存规则持久化
```bash
sudo iptables-save > /etc/iptables/rules.v4
```
> 规则默认重启丢失，`iptables-save` 导出后再配合 `iptables-persistent` 包实现持久化。

## 清空所有规则
```bash
sudo iptables -F
sudo iptables -X
```
> `-F` 清空所有链的规则，`-X` 删除用户自定义链，恢复到默认策略状态（通常是 ACCEPT）。
