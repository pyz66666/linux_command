# firewalld

## 查看状态和默认区域
```bash
sudo firewall-cmd --state
sudo firewall-cmd --get-default-zone
```
```
running
public
```
> firewalld 正在运行，默认区域是 public（网卡 eth0/wlan0 绑定到此区域）。

## 查看当前区域配置
```bash
sudo firewall-cmd --list-all
```
```
public (active)
  target: default
  interfaces: eth0 wlan0
  services: dhcpv6-client ssh
  ports: 80/tcp 443/tcp
  forward: yes
  masquerade: no
  rich rules:
```
> public 区域放行了 SSH、HTTP(80)、HTTPS(443)，启用了 IP 转发，未启用 NAT。

## 永久开放端口
```bash
sudo firewall-cmd --permanent --add-port=8080/tcp
sudo firewall-cmd --reload
sudo firewall-cmd --list-ports
```
```
success
success
80/tcp 443/tcp 8080/tcp
```
> `--permanent` 写入持久化配置加 `--reload` 后 8080/tcp 永久生效且不中断已有连接。

## 临时添加服务
```bash
sudo firewall-cmd --add-service=http
```
```
success
```
> 不加 `--permanent` 只运行时生效，重启或 `--reload` 后丢失。

## 使用 Rich Rule 封禁 IP
```bash
sudo firewall-cmd --add-rich-rule='rule family="ipv4" source address="10.0.0.99" drop'
```
```
success
```
> Rich Rule 提供比 `--add-port` 更精细的控制，这条规则直接丢弃来自 10.0.0.99 的所有包。

## 查看所有可用服务
```bash
firewall-cmd --get-services | tr ' ' '\n' | head -10
```
```
amanda-client
bacula
bgp
dhcp
dhcpv6
dns
docker-registry
dropbox-lansync
finger
ftp
```
> 列出 firewalld 预定义的所有服务名称，每个对应 `/usr/lib/firewalld/services/` 下的 XML 文件。
