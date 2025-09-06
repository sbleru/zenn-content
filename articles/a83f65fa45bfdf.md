---
title: "Google Cloudの覚えのない課金への対処"
emoji: "📘"
type: "tech"
topics: []
published: true
published_at: "2023-10-02 22:00"
---

# コンテキスト

- Google Cloud で少額の課金（17円ほど）が発生していた
	- 「Networking Service Directory Registered Resource」 に対しての課金
- 覚えがないので、原因特定して課金を止めたい
	- Google Cloudで遊んでた覚えはある

# やったこと

ほぼこちら（ありがたい）の手順ですが、若干のハマりあったので補足します。

[GKEのクラスタを削除してもネットワークサービスで課金が止まらない場合の対処法](https://zenn.dev/ikechan0829/articles/gcp_stop_billing_deleted_gke_cluster)


## Service Directory を確認する


↑記事通り、[Network -> Service Directory](https://console.cloud.google.com/net-services/service-directory/services/list) を確認すると、APIが無効になっておりサービスが確認できませんでした。

![](https://storage.googleapis.com/zenn-user-upload/9a90406b17f7-20231002.png)

ここが課金対象ではないかと思いましたが、APIを有効にしてみると、上記記事通り、名前空間「goog-psc-default」が存在していました。
※有効にしなくても、gcloud cliで確認できたのかも

## Service Directory の名前空間の削除

Google Cloud のコンソールでは削除できないので、gcloud cliを利用する

事前準備
```sh
# authの設定をしていない場合
gcloud config set account <your account email>
# projectの設定をしていない場合
gcloud config set project <target project>
```

service directoryを確認する。
```sh
# location は名前空間が作成されているRegion
gcloud service-directory namespaces list --location=asia-northeast1
```

service directoryを削除する
```sh
gcloud service-directory namespaces delete goog-psc-default --location=asia-northeast1
```

