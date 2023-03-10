+++
title = "Keychron K8 (ノンバックライト) 改造ログ"
date = 2022-11-03

[taxonomies]
tags = ["キーボード"]
+++

キーボード、いいですよね。

自作PCから自作キーボード関連の情報を見るようになり、
キーボード、特にメカニカルキーボードに興味を持つようになりました。

そんなこんなでKeychron K8 (ノンバックライト)茶軸を買いました。

文字を打ち込んで楽しんでいたのですが、段々下記の点が気になり始めました。

- わずかに金属音が響く
    - 一部のキーを押すとキーンと音が響く感じ
- 打鍵音が割と大きい
    - コンッといった打鍵感

それで巷の動画やサイトを見ていたら、どうやらルブや中にフォームを敷き詰めたりなどで改善するらしいぞ、
とのことで一念発起して我が家のKeychronに改造を施すことにしました。

**※注意：商品を分解すると返品と保証が無効になります。改造や分解に関して当サイトは一切の責任を負えませんので、あらかじめご了承ください。**

## フォームを敷く

まず、キーキャップとキースイッチを全部外します。
（分解してフォームを敷くだけなら全部である必要はないかもしれません。）

次に、Keychron K8を分解します。

アルミニウムフレームバージョンには、フレームのねじ止めに六角のねじが使われているため、分解には六角の形のドライバーが必要です。

また、PCBとプレートをねじ止めしているねじは少し小さめのため、
精密ドライバーセット等を持っていると便利だと思います。

分解方法は「Keychron K8 分解」等で調べると出てくる、公式のこれが参考になります。
- [Disassemble Process for K8](https://keychron.jp/pages/disassemble-process-for-k8)

分解しPCBを取り外すと、バッテリーとPCBがコードでつながっています。
慎重に取り外してください。

そしたら、ケースの底にスポンジや吸音材を敷き詰めます。
私はAmazonでNRスポンジ(3mm)を買って2層敷き詰めました。

バッテリー部分にはスポンジを置いてももしかしたら問題ないのかもしれませんが、
怖かったのと置いていない人が多かったため、置きませんでした。

敷き詰め終わったら、分解したPCBやプレート、フレームをもとに戻しましょう。

この時、私は一回右部のライトをちゃんとはめずに組みなおしてしまいました。
（次の日気づいて直しました。）

皆さんは気を付けましょう。

## キースイッチにルブをする

外したキースイッチにルブをします。

ルブにはまず下記が必要です。

- 潤滑剤（Krytox GPL 205、Krytox GPL 105、Tribosys 3204等）
- 筆またはマイクロアプリケータ

後は下記もあるといいと思います。

- スイッチオープナー
    - キースイッチを手で空けるの大変
- ステムホルダー
    - ステムにルブをするときにやりやすい

今回私がルブする対象はタクタイルスイッチだったため、
バネ用にKrytox GPL 105、それ以外用にTribosys 3204を遊舎工房で購入しました。

また、スイッチオープナーとステムホルダー、筆はセットになっているものがAmazonであったためそちらを購入しました。
色々あるので好きなのを購入するといいと思います。

最近はこういった道具が日本で手に入れやすくなったので、とても便利ですね。

ルブの仕方は色んなサイトや動画で紹介されているのでそれらを参考にするとよいと思いますが、
特に下記がまとまっていてよいと思います。

- [キースイッチベストプラクティス - recompile keys](https://keys.recompile.net/docs/keyswitch-best-practice/)

## キーキャップを変える

これは特に必要ないと思いますが、個人的にかわいいと思うキーキャップを見つけてしまったため、
これまた遊舎工房で購入して付け替えました。

![キーボード](/keyboard.jpg)

買ったのはAkko 9009 Retroです。地味目ですが、アクセントのピンクが特にかわいいと思っています。

ただ、完全にしっくり来たわけじゃないので、別の色に付け替えたり、
他に新しいキーキャップが欲しくなったらそっちに変えるかもしれません。

## 改造を終えて

改造の結果としては以下の通りとなりました。

- キーンという金属音がほとんどなくなった。
    - これは個人的にルブをしたおかげでバネ鳴りがなくなったのではないかと推測します。
- 音の響きが控えめになった。
    - カンッといった音だったのが、コトコトとした音に変わった。
- キーの動きが少し滑らかになったかも。
- 他の音が控えめになった影響かカサカサ音が少し気になるように。
    - ただキーキャップなしだと聞こえないため、キーキャップによって変わるかも。

おおよそ満足いったため、しばらくキースイッチを取り替えたりなどは控えようと思います。
（お金もかかるしね…。）

全体的には打鍵感がコトコトした感じになって、文字を打つのが楽しくなりました。
この文章を書いたのも、キーボードを使いたかったからですね。

作業の感想としては、

- キースイッチ抜くの痛い、大変。
- ルブはとても時間がかかる。
- でも思ったより楽しかった。
- 結果がわかりやすかったため、やっている途中でもやる気がわいてきた。
- ルブはかなり結果が変わるため、1回やってみると面白いかも。

思ったより自分は単純作業が好きなのかもしれないなあ、とか思いながらルブしてました。
色々やってみるのは面白かったので、いつかは自作キーボードにも手を出してみたいですね。
（今は場所がないためやりませんが）

この文章は、Keychron K8で書きました。