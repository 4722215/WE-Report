# 第8回　Webエンジニアリング演習　レポート

## 学籍番号 4722215

## 実装内容
```
@app.put("/todos/{todo_id}", response_model=TodoItem_Pydantic)
async def update_todo(todo_id: int, req: TodoItemUpdate_Pydantic):
    todo = await TodoItem.get(id=todo_id) #指定したIDのTODOアイテムを更新する
    if not todo:
        raise HTTPException(status_code=404, detail=f"ID {todo_id} のTODOが見つかりません") #指定されたIDがないとき、404エラーを返す

#更新したTODOアイテムをレスポンスとして返す
    todo.title = req.title if req.title is not None else todo.title
    todo.description = req.description if req.description is not None else todo.description
    todo.completed = req.completed if req.completed is not None else todo.completed
    await todo.save()
    return todo
```

## 動作確認
### 存在するIDを指定した場合
```
Request:
curl -X 'PUT' \
  'http://127.0.0.1:8000/todos/1' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "title": "string",
  "description": "string",
  "completed": false
}'
Response:
{
  "id": 1,
  "title": "string",
  "description": "string",
  "completed": false
}
```

### 存在しないIDを指定した場合
```
Request:
curl -X 'PUT' \
  'http://127.0.0.1:8000/todos/-1' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "title": "string",
  "description": "string",
  "completed": false
}'

Response:
{
  "detail": "Object \"TodoItem\" does not exist"
}
```