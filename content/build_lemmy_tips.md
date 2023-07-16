+++
title = "Lemmy鯖建設・運用時にはまったところ"
date = 2023-02-16

[taxonomies]
tags = ["Lemmy", "サーバー"]
+++

こんにちは。

何日か前にここLemmy鯖を建てたのですが[（ここ）](https://lem.simple-gear.com)、その際とその後の稼働時にはまったところがいくつかあったため、記録しようと思います。

（人によってはこんなとこはまらんだろ…ってところもあるかもしれませんが）

## ansibleで最初構築しようとしたらうまくいかなかった

言い訳すると[公式ドキュメント](https://join-lemmy.org/docs/en/administration/administration.html)にはAnsibleでの構築を推奨ってあったんですよね…。

> We recommend using Ansible, because it simplifies the installation and also makes updating easier.

どうもLemmy自体の更新にドキュメント更新が追い付いていないようで、上記部分以外にも古い内容がいくつかあったようです。

ここについては今現在（2023/3/2）ではAnsibleでの構築が非推奨のようなので注意が必要です。

## nginxをDockerで一緒に動かそうとしたらうまくいかなかった

こちらは原因が未だによく分かってないです。

この鯖を建てようとしたときは0.17.1が最新だったため、こちらのdocker-compose.ymlを参考に最初は建てようとしたのですが、どうにもうまくいきませんでした。

参考：https://github.com/LemmyNet/lemmy/blob/0.17.1/docker/prod/docker-compose.yml

現在動いている鯖は結局、nginxはDocker外に出し動かしています。

この時のdocker-compose.ymlは0.16の頃のものを参考にしました。

参考：https://github.com/LemmyNet/lemmy/blob/0.16.7/docker/prod/docker-compose.yml

同様に上記を参考にする場合は、lemmy-uiの環境変数が0.17.0で変更されているため、気を付けましょう（一敗）

参考：https://github.com/LemmyNet/lemmy/blob/main/RELEASES.md#lemmy-v0170-release-2023-01-31

## Mastodonからここのコミュニティが認識されない他

上記問題を解決し、うわーやっとちゃんと建った！と思ったら、MastodonからURLで検索してもここの鯖のコミュニティが出てきていませんでした。

ここは何日か詰まったのですが、最終的に下記issueを参考にnginxの設定を変更したら解決しました。

参考：https://github.com/LemmyNet/lemmy/issues/1909

下記ビフォーアフターです。

#### before

```
if ($http_accept = "application/activity+json") {
    set $proxpass "http://0.0.0.0:8536";
}
if ($http_accept = "application/ld+json; profile=\"https://www.w3.org/ns/activitystreams\"") {
    set $proxpass "http://0.0.0.0:8536";
}
```

#### after

```
if ($http_accept ~ "^application/.*$") {
    set $proxpass "http://0.0.0.0:8536";
}
```

おそらくMastodonからのアクセス時にbeforeの方だとバックエンドの方のアクセスにならず、それが原因で認識しなかったのではないかと予想しています。（ちゃんと調べてはいない）

## おわりに

そんなこんなで何とか動かしているここLemmy鯖ですが、この度0.17.2にアップデートもし、Mastodon連携等色々やれることも増えて中々楽しませていただいています。

その内、テーマも作成してかえられたらなぁと考えています。
いつになるかはわかりませんが…。

以上、読んでいただきありがとうございました。
