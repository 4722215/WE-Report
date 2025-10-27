# 第5回　Webエンジニアリング演習　レポート

## 学籍番号 4722215

## 各エンドポイントのSwagger UIでのテスト結果
### GET / read_root
```
Request:
curl -X 'GET' \
  'http://127.0.0.1:8000/' \
  -H 'accept: application/json'

Response:
{
  "Hello": "World"
}
```
### GET / health_check
```
Request:
curl -X 'GET' \
  'http://127.0.0.1:8000/health' \
  -H 'accept: application/json'

Response:
{
  "atatus": "healthy"
}
```
### GET / read_item
```
Request:
curl -X 'GET' \
  'http://127.0.0.1:8000/items/1?q=test' \
  -H 'accept: application/json'

Response:
{
  "item_id": 1,
  "q": "test"
}

負の値を設定してテスト
Request:
curl -X 'GET' \
  'http://127.0.0.1:8000/items/-1?q=test' \
  -H 'accept: application/json'

Response:
{
  "detail": "Item ID must be positive"
}
```