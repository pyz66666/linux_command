# tar

## 打包并 gzip 压缩
```bash
tar -czf project.tar.gz ./project/
```
```
```
> `-c` 创建、`-z` gzip 压缩、`-f` 指定文件名，生成 `.tar.gz` 压缩包。

## 解压到指定目录
```bash
tar -xzf archive.tar.gz -C /opt/app/
```
```
```
> `-x` 解压、`-C` 指定目标目录，目录不存在会自动创建。

## 不解压只查看内容
```bash
tar -tzf backup.tar.gz
```
```
home/user/docs/report.txt
home/user/docs/notes.md
home/user/images/logo.png
home/user/images/banner.jpg
home/user/config/settings.conf
```
> `-t` 列出归档中所有文件路径，方便解压前确认内容。

## 打包并排除特定文件
```bash
tar -czf src.tar.gz --exclude='*.log' --exclude='node_modules' ./src/
```
```
```
> `--exclude` 跳过匹配的文件和目录，减少归档体积。

## 解压并显示详情
```bash
tar -xzvf archive.tar.gz
```
```
home/user/docs/report.txt
home/user/docs/notes.md
home/user/images/logo.png
```
> `-v` 解压时显示每个被提取的文件名。

## 创建 .tar.xz 压缩包
```bash
tar -cJf project.tar.xz ./project/
```
```
```
> `-J` 使用 xz 压缩，比 gzip 压缩率更高但更慢。
