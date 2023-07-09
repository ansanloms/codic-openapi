すべての API アクセスには、アクセストークンをリクエストヘッダーに含める必要があります。アクセストークンは[サインアップ](https://codic.jp/signup)後、API ステータスのページで確認できます。アクセストークンは、ユーザーを識別する情報のため適切に管理してください。また定期的にリセットすることをおすすめします。

```
GET /v1/xxx.json HTTP/1.1
Host: api.codic.jp
Authorization: Bearer YOUR_ACCESS_TOKEN
```
