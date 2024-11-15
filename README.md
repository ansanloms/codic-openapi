# codic-openapi

[Codic API](https://codic.jp/docs/api) の [OpenAPI](https://www.openapis.org/) 定義(Unofficial)。

## API リファレンス

codic API は、codic のリソースへアクセスするための RESTful (JSON) なインタフェースをアプリケーション開発者へ提供します。API を利用するためには、[アクセストークン](https://codic.jp/docs/api#authorization)が必要です。

### ホスト

すべての API リクエストは、以下のホストを経由して提供されます。

```
https://api.codic.jp
```

### アクセス制限

リソースを公平に分配するため、一定時間アクセス可能な回数に制限があります（レートリミットと言います）。最大アクセス数はプラン毎に異なります。最大アクセス数を超えてしまった場合は、API ステータスのページよりリセットしてください。

### 認証

すべての API アクセスには、アクセストークンをリクエストヘッダーに含める必要があります。アクセストークンは[サインアップ](https://codic.jp/signup)後、API ステータスのページで確認できます。アクセストークンは、ユーザーを識別する情報のため適切に管理してください。また定期的にリセットすることをおすすめします。

```
GET /v1/xxx.json HTTP/1.1
Host: api.codic.jp
Authorization: Bearer YOUR_ACCESS_TOKEN
```

### レスポンスコード

成功時レスポンスコード 200 を返します。エラーが発生した場合、API は 400, 500 番台のエラーコードと共に、エラー情報を返します。以下はエラー時の JSON レスポンスの例です。

```json
{
  "errors": [
    {
      "code": 404,
      "message": "ページが存在しません。",
      "context": null
    }
  ]
}
```

### バージョンアップポリシー

構造の変更、フィールドの削除などの改訂については、異なるバージョンとしてリリースされるため、クライアントが考慮すべき事はありませんが、フィールドの追加については同一バージョンで行うため、想定しないフィードルが出現した場合に、エラーとならないように考慮してください。
