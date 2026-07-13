# docker inspect

## 查看容器完整信息
```bash
docker inspect web
```
```
[
  {
    "Id": "d3f7a8b9c1e2...",
    "State": { "Status": "running", "Running": true, "Pid": 12345 },
    "NetworkSettings": {
      "IPAddress": "172.17.0.2",
      "Ports": { "80/tcp": [{ "HostPort": "8080" }] }
    },
    "Mounts": [{
      "Source": "/host/data",
      "Destination": "/app/data"
    }]
  }
]
```
> 返回 JSON 格式的完整容器元数据，包含状态、网络配置、挂载信息等所有细节。

## 提取特定字段
```bash
docker inspect -f '{{.State.Status}}' web
```
```
running
```
> `-f` 用 Go 模板格式提取想要的字段，避免在大量 JSON 中找信息。

## 查看容器 IP 地址
```bash
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' web
```
```
172.17.0.2
```
> 用 `range` 遍历多网络配置，提取容器的内网 IP。

## 查看镜像信息
```bash
docker inspect nginx:alpine
```
```
[
  {
    "Id": "sha256:d3f7a8b9c1e2...",
    "Created": "2026-07-10T08:00:00Z",
    "Size": 41000000,
    "Architecture": "amd64",
    "Os": "linux"
  }
]
```
> 查看镜像的创建时间、大小、架构等信息，帮助排查兼容性问题。
