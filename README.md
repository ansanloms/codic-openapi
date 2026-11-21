# codic-openapi

[Codic API](https://codic.jp/docs/api) の [OpenAPI](https://www.openapis.org/) 定義(Unofficial)。

## API リファレンス

codic API は、codic のリソースへアクセスするための RESTful (JSON) なインタフェースをアプリケーション開発者へ提供する。API を利用するためには、[アクセストークン](https://codic.jp/docs/api#authorization) が必要である。

### ホスト

すべての API リクエストは、次のホストを経由して提供される。

```
https://api.codic.jp
```

### アクセス制限

リソースを公平に分配するため、一定時間アクセス可能な回数に制限がある（レートリミットと言う）。最大アクセス数はプラン毎に異なる。最大アクセス数を超えてしまった場合は、API ステータスのページよりリセットすること。

### 認証

すべての API アクセスには、アクセストークンをリクエストヘッダーに含める必要がある。アクセストークンは [サインアップ](https://codic.jp/signup) 後、API ステータスのページで確認できる。アクセストークンは、ユーザーを識別する情報のため適切に管理すること。また定期的にリセットすることをおすすめする。

```
GET /v1/xxx.json HTTP/1.1
Host: api.codic.jp
Authorization: Bearer YOUR_ACCESS_TOKEN
```

### レスポンスコード

成功時レスポンスコード 200 を返す。エラーが発生した場合、API は 400, 500 番台のエラーコードと共に、エラー情報を返す。以下はエラー時の JSON レスポンスの例である。

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

構造の変更、フィールドの削除などの改訂については、異なるバージョンとしてリリースされるため、クライアントが考慮すべき事はないが、フィールドの追加については同一バージョンで行うため、想定しないフィードルが出現した場合に、エラーとならないように考慮すること。

## 開発

- `.node-version` に書かれたバージョンの Node が必要。
- `npm ci`: 依存を入れる。
- `npm run lint`: 型検査、oxlint と oxfmt、textlint、redocly lint を順に実行する。
- `npm test`: `bin/` 配下のスクリプトのテストを実行する。
- `npm run fix`: sort と textlint、oxlint、oxfmt の各 fixer を順に実行して最後に lint する (途中で失敗しても続行)。
- `npm run build`: `dist/` に `index.html` (Redoc の JS を埋め込んだ単一の HTML) と `api.yaml` を出力する。
- `npm run dev`: Vite の dev サーバを `http://localhost:4000` で起動する。dev サーバは spec を `redocly build-docs` で HTML にして返す。spec のファイルを編集すると HTML が作り直され、ブラウザが再読み込みされる。

依存は `.npmrc` により正確な版で固定する。自前の 2 パッケージ (textlint-plugin-yaml-keys、redocly-plugins) は GitHub のタグを git 依存で参照しており、Dependabot が更新しないため `package.json` のタグを手で書き換えて `npm install` する。
