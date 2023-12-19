# traQ_deploy_sample

[traQ](https://github.com/traPtitech/traQ) を [deployment.md](https://github.com/traPtitech/traQ/blob/master/docs/deployment.md) に従って https://localhost:8080/ にデプロイするサンプル

## デプロイ方法

1. サーバーを確保する
2. サーバー上にDockerをインストール
3. このレポジトリをclone
4. `docker compose up -d`

### インターネットから接続できるようにする

1. サーバーの80番、443番ポートを解放する（レンタルサーバーサービス側の設置とか、iptablesとか）
2. 固定IPをとる
3. ドメインをとり、IPを登録する
4. `Caddyfile` に書かれている `localhost` をドメイン名にする(`example.com`等)
5. `config.yml` に書かれている `https://localhost` をドメイン名にする(`https://example.com`等)
6. `compose.yml`に書かれている `reverse-proxy`の`ports`を`"8081:80"` `8080:443` から、`"80:80"` `443:443` に変更する
7. dockerコンテナを再起動する `docker compose stop; docker compose up -d`

### サーバースペックについて

(2023/12月現在) ユーザー数が1桁の場合はこのような印象です。
* CPU: 画像投稿時以外は余裕があります。
* Memory: es拡張が 1GB、他(reverse-proxy,backend,frontend,widget,db)が合わせて1GB程度あれば十分です。
