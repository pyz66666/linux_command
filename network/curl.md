# curl

## GET 请求获取网页内容
```bash
curl https://httpbin.org/get
```
```
{
  "args": {},
  "headers": {
    "Host": "httpbin.org",
    "User-Agent": "curl/7.81.0"
  },
  "url": "https://httpbin.org/get"
}
```
> 最基础的 GET 请求，`curl` 默认使用 GET 方法，响应直接输出到终端。

## 查看响应头
```bash
curl -I https://www.example.com
```
```
HTTP/2 200
content-type: text/html; charset=UTF-8
content-length: 1256
server: nginx/1.24.0
date: Sat, 12 Jul 2026 10:00:00 GMT
cache-control: max-age=604800
```
> `-I` 只获取响应头（HEAD 请求），快速检查 HTTP 状态码、服务器类型和缓存策略。

## POST JSON 数据
```bash
curl -X POST https://httpbin.org/post \
  -H "Content-Type: application/json" \
  -d '{"name":"Alice","email":"alice@example.com"}'
```
```
{
  "json": {
    "email": "alice@example.com",
    "name": "Alice"
  },
  "url": "https://httpbin.org/post"
}
```
> `-X POST` 指定方法，`-H` 设置请求头，`-d` 发送 JSON 请求体，是 REST API 调试的标准写法。

## 下载文件
```bash
curl -L -O https://github.com/user/repo/releases/download/v1.0/app.tar.gz
```
```
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 50.0M  100 50.0M    0     0  12.5M      0  0:00:04  0:00:04 --:--:-- 12.5M
```
> `-L` 跟随重定向，`-O` 以远程文件名保存到本地，进度条显示下载速度和完成百分比。

## 调试请求详情
```bash
curl -v https://api.example.com/health
```
```
*   Trying 93.184.216.34:443...
* Connected to api.example.com (93.184.216.34) port 443
> GET /health HTTP/2
> Host: api.example.com
> user-agent: curl/7.81.0
>
< HTTP/2 200
< content-type: application/json
<
{"status":"ok","uptime":86400}
```
> `-v` 显示完整的请求（`>`）和响应（`<`）头，包括 TLS 握手细节，是排查 API 问题的利器。

## 上传文件
```bash
curl -F "file=@/path/to/image.png" https://upload.example.com/
```
```
{
  "files": {
    "file": {
      "filename": "image.png",
      "size": 245760,
      "type": "image/png"
    }
  }
}
```
> `-F` 以 multipart/form-data 方式上传文件，`@` 后跟本地文件路径。
