# jq

## 格式化 JSON
```bash
echo '{"name":"Alice","age":30}' | jq '.'
```
```
{
  "name": "Alice",
  "age": 30
}
```
> `.` 表示根对象，jq 自动格式化并语法高亮 JSON。

## 提取字段值
```bash
echo '{"name":"Alice","age":30}' | jq '.name'
```
```
"Alice"
```
> `.name` 提取 name 字段的值，默认输出带双引号的 JSON 字符串。

## 提取原始值（去引号）
```bash
echo '{"name":"Alice","age":30}' | jq -r '.name'
```
```
Alice
```
> `-r` 输出原始字符串，去掉 JSON 引号，适合赋值给 shell 变量。

## 遍历数组
```bash
echo '[{"name":"Alice"},{"name":"Bob"}]' | jq '.[].name'
```
```
"Alice"
"Bob"
```
> `.[]` 展开数组，对每个元素取 `.name` 字段。

## 条件过滤
```bash
jq '.items[] | select(.price > 100)' products.json
```
```
{
  "name": "Widget Pro",
  "price": 150
}
{
  "name": "Super Gadget",
  "price": 200
}
```
> `select(.price > 100)` 只保留 price 大于 100 的数组元素。

## 构造新 JSON 对象
```bash
jq '{name: .name, email: .email}' data.json
```
```
{
  "name": "Alice",
  "email": "alice@dev.com"
}
```
> 从原始 JSON 中提取多个字段，组成新的 JSON 对象。

## 统计数组长度
```bash
jq '.items | length' data.json
```
```
5
```
> `length` 返回数组元素个数。
