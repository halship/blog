+++
title = "Mastodonおひとり様サーバーを建てました"
date = 2022-11-27

[taxonomies]
tags = ["Mastodon", "サーバー"]
+++

11/17にmastodon-japan.net（通称じゃぱねっと鯖）にアカウントを作成した私

- [@halship@mastodon-japan.net](https://mastodon-japan.net/@halship)

は、
鯖缶の人たちなどをフォローしたことで刺激を受け、
11/21におひとり様サーバーを建てました。

- ~~simple gear don~~
- →2023/07/16追記: 潰したり建てたりして今はここです [https://akm.simple-gear.com](https://akm.simple-gear.com)

おひとり様なのでユーザ登録を受け付けていません、ごめんね。

建設までは色々あったので、かるーくまとめてみます。
かるーくなのであまり参考にはならないと思います。

## まずは公式ドキュメントを見る

Mastodonの公式ドキュメントがすごく参考になります。
これ見てればMastodon自体のインストールは大体うまくいく感じです。

- [Mastodon documentation](https://docs.joinmastodon.org/)

## ドメインを買った

期間限定で安かったので適当なドメインをお名前.comにて0円で買いました。
今のところ、メールがめっちゃきてうざいです。

DNSの設定とかサブドメインの管理とかを全部こっちで結局やっています。
このブログのドメインもこれです。

## VPSを借りた

EC2やOCIなんかでもよかったのですが、
従量課金がこわくて結局CPU3コア・メモリ2GのVPSにしました。

どこでもよかったのですが、初回割引で割と安かったConoHaにしました。
1年分契約したので1年はそのままですが、
サポートや安定性があまりにも悪かったら次年は移行を考えてもいいかもしれません。

今のところ問題なく使えています。

VPSを立ち上げたら、最初にユーザ設定やらSSH接続設定やらセキュリティ設定をやるといいと思います。
ConoHaだったら[ここ](https://support.conoha.jp/vps/guide/vpsstartup/?btn_id=v-sudo-sidebar_guide-vpsstartup)とかを参考に。

Mastodon公式ドキュメントにもセキュリティ的な話が書いてあるので参考にしましょう。
- [Preparing your machine - Mastodon documentation](https://docs.joinmastodon.org/admin/prerequisites/)

## AWSでS3バケットを作成した

AWSへの登録はちょっと前にしていたのですが、
ここでメディアファイルを格納するためのS3バケットを作成しました。

おひとり様なのでもしかしたらそこまでする必要はないかもしれないのですが、
後からS3に移行しようとすると大変と聞いていたため準備しました。

最初は設定を変えずに作成したのですが、最終的な設定内容としては以下の通りになりました。

- バケット自体は非公開
- 静的ウェブサイトホスティング：無効
- ACL：有効
- Mastodon専用アカウント経由でのアクセスを許可
- ブロックパブリックアクセス：「任意のアクセスコントロールリスト (ACL) を介して付与されたバケットとオブジェクトへのパブリックアクセスをブロックする」のみオン
- CORSを設定

うまくいかないなーここかなー的な感じで設定をしていったため、
必要じゃない設定が含まれているかもしれません。
ですのでここら辺に関しては特に参考にならないと思います。
また、CloudFront経由での配信をがっつり想定して設定していったため、
経由しない場合はもっとシンプルになるとは思います。
（でもCloudFrontとかかませないと色々こわい）

先人の以下のような記事がありますので、そちら等を参考にしたほうがいいと思います。

- [Mastodon v3.2.0 アップデートメモ (S3+CloudFront環境)](http://www.shibafu528.info/2021/03/mastodon-v320-s3cloudfront.html)
- [メディアの配信にCloudFrontを採用しました](https://diary.akane.blue/2020/10/01/cloudflare-to-cloudfront/)
- [Mastodon の画像などメディアデータをAmazon S3に移行する（非Docker環境）](https://takanory.hatenablog.jp/entry/2017/05/10/070000)

## CloudFrontを設定した

設定では、OAC（Origin Access Control）を使用しました。

設定の中で独自ドメインを設定することができるのですが、
こちらには証明書が必要となりますので、
ACMを使って設定したいドメインの証明書を発行してもらわなければなりません。

手順通りに証明書を発行したら、次はドメインを買ったところ（ここではお名前.com）にて、CNAMEの設定をします。

|NAME                 |VALUE                        |
|:--------------------|:----------------------------|
|media.simple-gear.com|xxxxxxxxxxxxxx.cloudfront.net|

あとやったこととしては、media.simple-gear.com内に存在しないファイルを開こうとした際に404ページが開くよう設定しました。

![スクリーンショット1](/screen01.png)

(こんな感じ)

この辺の設定については[ここ](https://aimstogeek.hatenablog.com/entry/2018/07/23/135032)らへんを参照するといいと思います。

## メールサーバを設定した

自分でやるのはつらすぎなので、私はSendGridを使いました。
承認を得るまでの期間があるため気を付けましょう。

## Mastodonをサーバーにインストールした

ここまで来たら、後はインストールです。
といっても、手順は公式ドキュメント通りにやっていけば特に問題なく終わると思います。

唯一はまったのは、「Setting up nginx」項の```systemctl reload nginx```でした。
今はもう忘れてしまったのですが、おそらく証明書関係の部分でエラーが起きてリロードできなかったんだと思います。

ずばりな解決策があったので、リンクを張っておきます。

- [mastodonの鯖を建てたので、その覚書(主に公式ドキュメントに対する)](https://qiita.com/tatmius/items/6d839ef307d040bf2727)

抜粋すると、こちらの
```
systemctl stop nginx
certbot certonly --standalone -d example.com
```
を実行し、```/etc/nginx/sites-available/mastodon```の次の2行をアンコメントです。
```
# ssl_certificate     /etc/letsencrypt/live/example.com/fullchain.pem;
# ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;
```

## 建設完了

ここまでやった後、設定したドメインにアクセスしてみて下記の画面のように（これは一部ですが）なったらMastodonはひとまず建ちあがったのだと思います。

![マストドンOK](/ok_mastodon.png)

逆に以下のような画面が出たら何かエラーが起きています。
[Mastodonのトラブルシューティング](https://docs.joinmastodon.org/admin/troubleshooting/)を参考に原因を調べましょう。

![マストドンNG](/ng_mastodon.png)

因みに私は単にMastodonが使うポートを開けそびれていただけでした。てへぺろ。

## 終わりに

ネットワークやサーバーの仕組みをほとんど知らない状態から、
色々調べつつ1つのMastodonサーバーを動かしたのはとても楽しかったです。

楽しかったで終わらず、継続してこちらのサーバー運用をしていきたいと思います。

あ、よかったらフォローしてみてね。

- ~~@halship@mstdn.simple-gear.com~~
- →2023/07/16追記: 今はここ [@halship@akm.simple-gear.com](https://akm.simple-gear.com/halship)
