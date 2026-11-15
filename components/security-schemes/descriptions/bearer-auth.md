すべての API アクセスには、アクセストークンをリクエストヘッダーに含める必要がある。アクセストークンは [サインアップ](https://codic.jp/signup) 後、API ステータスのページで確認できる。アクセストークンは、ユーザーを識別する情報のため適切に管理すること。また定期的にリセットすることをおすすめする。

```
GET /v1/xxx.json HTTP/1.1
Host: api.codic.jp
Authorization: Bearer YOUR_ACCESS_TOKEN
```
