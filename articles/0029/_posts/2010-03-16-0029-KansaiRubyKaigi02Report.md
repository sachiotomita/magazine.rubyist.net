---
layout: post
title: RegionalRubyKaigi レポート (11) 関西 Ruby 会議 02
short_title: RegionalRubyKaigi レポート (11) 関西 Ruby 会議 02
tags: 0029 KansaiRubyKaigi02Report
---


書いた人: Tagawa

## はじめに

11/7、11/8 の 2 日間にわたって関西 Ruby  会議 02 が開催されました。

今回の開催形態は去年と同様に関西オープンソース 2009( 以下 KOF2009 と略記する)と共同開催としました。

* [関西 Ruby  会議 02](http://regional.rubykaigi.org/kansai02)
* [関西オープンソース 2009](http://k-of.jp/2009/)


発表者は関西圏に留まらず、東京都や島根県・果てははるばるカナダのバンクーバーから駆けつけていただきました。
おかげさまで、どの講演も会場はほぼ満員という大盛況になり、関西における Ruby  の関心の高さを伺わせる結果となりました。

## 関西 Ruby  会議 02 について

開催日
: 1 日目：2009 年 11 月 6 日 (金) 13:00 〜 18:00<br />2 日目：2009 年 11 月 7 日(土) 10:00 〜 18:00

開催場所
: 大阪南港 ATC ITM 棟 6F マーレギャラリー

開催母体
: Ruby  関西

## 11/6 (金) の発表内容

### 続・現場で役立つ Ruby  on Rails パターン

#### 参加者数

* 約 50 名
  * 最初は 40 人ぐらいでしたが、最終的にほぼ満席になりました。


#### 発表者

* 大場寧子さん


#### 発表内容

一番最初の発表は株式会社万葉の大場寧子さんにしていただきました。
お話しされた内容は大きく分けると以下の内容です。

1. 株式会社万葉の紹介
1. Ruby  での開発方法
1. Ruby Kaigi2009 でのお話のおさらい
1. 本当は奥が深い検証の話
1. RESTful との付き合い方


##### 万葉の紹介

  * 家計簿ソフト「小槌」
  * iPhone 用のカルタソフト「iCarta」
  * Rails  用の Plugin
  * グループウェア「ナレジオン」


等の開発をされているそうです。

##### Ruby  での開発方法

基本は Agile っぽく動かしているのですが、開発人数が Rails  の開発にしては多い方なので、
開発体制を工夫されていると仰っていました。
その中で、特にメンバー間の「合意作りが大事」だと強調されていました。メンバーの合意を得られるためには、

* 誰もが決められるようにしておく
* 勝手に既成事実化しない


ということを守ることが必要とも仰っていました。

##### Ruby  会議 2009 でお話しされたことのおさらい

* 如何に変更しやすくするか
* 如何にコードを良い状態に保つか


ということをかいつまんで説明されていました。

##### 本題に入る前に

1. Ruby  をよく使っている人
1. Rails  をよく使っている人


についてどれぐらい居るのか質問されました。

* Ruby  をよく使っている人は部屋の中の8割ぐらい
* Rails  をよく使っている人は部屋の中の3割ぐらい


の人が使っていらっしゃるようでした。

##### 本当は奥が深い検証の話

Rails  の入力検証は良くできていると仰り、その利点を述べられた後、以下の問題点が存在すると仰いました。

1. 乱用される
1. 検証ニーズが場合によって違う場合に困る


乱用される問題に対しては

* そもそもActiveRecordの検証とは何か


という定義のお話から始められ、
「ActiveRecordオブジェクトがユーザーに許可された操作によって不正な状態で永続化されないようにするための仕組み」
と定義され、特に「ユーザーに許可された操作によって」の部分が重要だと強調されていました。
そのため、
「モデルの検証」＞「validate(ActiveRecordの検証)」
であり、全ての「モデルの検証」に「validate(ActiveRecordの検証)」を使うのは誤りだと仰っていました。
解決策としてはActiveRecordの検証に当てはまらない「モデルの検証」には

* コールバックで例外を投げる
* コールバックで専用の例外を投げる


のが有効だと仰っていました。

更に酷い例として

* ActiveRecordの検証で「モデルの検証」だけでなく「コントローラのエラー処理」まで行っている


ものを挙げられました。
これは検証とエラー処理を混同されている例で、守備範囲外のものにまで検証を使ってはいけないと仰っていました。

次に検証ニーズが場合によって違う場合に困る場合についてお話しされました。

* モデルの検証は1パターンではないのにActiveRecordの検証の通り道は1パターン


なので、オブジェクトの状態によって場合分けをしないといけない。しかし、場合分けは意外と面倒で痛い目を見ることが多いと仰っていました。

これに対しては
モデルの様々な使い方を意識しておくべきと仰っていました。

##### RESTfulとの付き合い方

最初にRESTを使っているかどうか質問されたところ、会場内で使っている人は1/5〜1/6ぐらい人が使っていらっしゃるようでした。
まずはRESTについての簡単な説明をされました。

* URLはリソース(名詞)
* HTTPメソッドは操作(動詞)
* シンプルで統一された、人間も読む事の出来るI/F


Rails について行くにはRESTを使うのは不可避だと強調されていました。
RESTfulにすることの利点としては

* インターフェースがきれいになる
* 必要なインターフェースが予測可能になり、統一化できる
* インターフェースが保守しやすくなる


という点を挙げられていました。
ここでRESTと上手くつきあう方法として

1. Rails 的なツボ
1. RESTの基本
1. URLから考える
1. routes.rbの整理


の4点を挙げられていました。
Rails 的なツボは

* よくあるアクションのマッピングを楽にすること
* マッピングに名前をつけてURLの名前にする


RESTの基本は
リクエスト=名詞(URL)+動詞(HTTPメソッド)としてGET・POST・PUT・DELETEの4つの動詞で適切な動詞・名詞を選ぶことにあるそうです。
URLから考えることは
URLを設計してその後でコントローラを設計し、うまくコントローラを分割することだそうです。
次にroutes.rbの問題について取り上げられました。routes.rbは散らかしやすいので、

* with_optionsの活用
* コントローラ別に記述する
* sub_resourcesプラグインを使う


の3つの解決方法を提示されていました。
このなかで大場さんがお書きになったsub_resourcesプラグインについての説明をされました。

#### 発表資料

発表資料は以下のURLをご参照ください。
[ぷっちん日記](http://ko.meadowy.net/~nay/diary/20091109.html#p01)

#### 感想

Rails の深い話と断っていらっしゃった通り、かなりRails の内部に突っ込んだお話をされていました。Rails で開発を行うときにぶつかった問題とその解決方法をお話しいただけて、大変貴重な講演だったと思います。残念ながら盛りだくさんの内容なので、50分では時間が足りないと思われました。また一度じっくりとお話をお聞きしたい内容でした。

### Ruby でソフトウェアづくりをアジャイルにするということについて

#### 参加者数

* 約50名
  * いきなり最初から満席となりました。角谷さんの講演の人気の高さが伺えました。


#### 発表者

* 角谷信太郎さん


#### 発表内容

発表の日が金曜日ということもあって、一般向けでお話をされていました。さらりと自己紹介をされた後、今日伝えたいことして

* プログラムを書いたことのないシステムエンジニアが威張っている会社は早晩滅びる


の言葉を「ビューティフル・コード」の推薦の言葉から引用されました。

まず、ソフトウェアづくりとはなにかについて説明されました。
ソフトウェアづくりとは

1. 実行主体
1. プロセス
1. アクティビティ


の３つで成り立ち、「日々やっていく行為の連続である」と強調されていました。

ここで、話は建築家Christopher Alexanderの「The Nature of Order」のという本から
「美しいものはある種の構造と形を持っていて、それを形作るにはプロセスがある」という文章を引用されて、プロセスの定義として

* 少しずつ進んでいく
* 結果からフィードバックを受ける
* 最初から決まっているわけではない
* 全体というものを意識しないといけない


これがアジャイル開発と非常によく似ていると仰いました。

ここからソフトウェアの本質について、

* 価値…人とソフトウェアの間にある
* システム全体を構成する（ハード　ソフト　文書　運用）
* 変更に対応できることが前提（育てること　技術的負債）


プログラミングについて

* スキルを備えた人の活動
* 世界観を構築している
* 簡単なお仕事ではない


と話されていました。

更にプログラミングが世界観を構築しているとは

* コードにしたもの
* コードにしなかったもの


の2つを含むと仰い、したことはコードになっていても、しなかったことはコードを読んでも分からないことから、ドキュメント等を書くことの必要性を説かれました。

自然に作られたソフトウェア開発としてのオープンソース開発を挙げられ、

* オープンソースはバザールスタイルの開発であり、
  * 少しずつ進んでいく
  * 結果からフィードバックを受ける
  * 最初から決まっているわけではない


と関連があることを話されました。更に

* 全体というものを意識しないといけない
  * 全体を見渡すというよりも全体に貢献できるかどうか。


ということになるのではと話されました。

ここでアジャイル開発について言及されて、アジャイルとは「形容詞」である。アジャイル開発というモノは無い。日々のプロセスをどうアジャイルに近づけるかが重要であると述べられました。

では如何にしてアジャイル開発を実践するかの話に移られ、
「アート・オブ・アジャイル・デベロップメント」にある37のプラクティスを全部やればバグはなくなると話されました。しかし全て実践するのは無理なので、「Head First ソフトウェア開発」を参考にすると良いと仰いました。ここで

* 自分のチームと自分のプロジェクトにあうプロセスを選び、そのプロセスの


成果物が自分の顧客の要望に合うように調整すること。
が重要であると強調されました。
「自分のプロジェクトにあうプロセスを選び」の部分で良いプログラミング言語を選ばなければならないと仰い、Ruby が勧められました。その理由として
「Ruby のコミュニティーではきれいなコード・上手く設計されたオブジェクト指向設計・テストしやすさなどの良いプログラムの書く方法が「正統」になっている」
と仰いました。

「入門Git」の中から

* 「仕事のために」道具がある
  * Linusがやりたいことのをするために作られた
* 見えていないものの方が大きいし、重要
  * 人間はパターンを認識する動物であることが利点でもあり、罠でもある。表面のモノに惑わされがち。


と話されました。

最後にプログラマは重要な地位なので、

* プログラマは本来見積りや計画もしなければいけない。
* 持っている力を発揮出来るようにしなければならない。


そこで

* プログラムを書いたことのないシステムエンジニアが威張っている会社は早晩滅びる


の言葉を「ビューティフル・コード」の再度引用され、プログラマの考えるべきことはいまやコードだけにとどまらないと話を締めくくられました。

#### 感想

「プログラムを書いたことのないシステムエンジニアが威張っている会社は早晩滅びる」との言葉は最近あちこちで聞かれるようになりましたが、角谷さんのお話はそれに留まらず、だからこそプログラマはコードにならないものにも気を配らないといけないと強調されていると思いました。これは中々語られることのない貴重な発言だと思いました。
また、プログラム開発には「コードにしたもの」と「コードにしないとした判断」の2つを含むとの言葉には感銘を受けました。
オープンソース開発の「その辺に生えてくるのと同じ。野生ですよ」「ついかっとなって作ってしまった」の部分は場内大爆笑になりました。

#### 発表資料

発表資料は以下のURLをご参照ください。
[角谷HTML化計画](http://kakutani.com/20091106.html)

## 11/7 (土)

### Hacking parse.y

#### 参加者数

#### 発表者

* ujihisa さん


#### 発表内容

はるばるカナダのバンクーバーから駆けつけていただきました。

* 内容


Ruby のソースコードで最大の行数を誇るparse.yをHackしよう！というものでした。

* 目的


parse.yを書き換えて新しいシンタックスを追加し、それの動作確認によってparse.yひいてはRuby の内部を理解するというものでした。
ujihisaさんのお話によると「初めてRuby の中を触るという人向けの話」だそうです。

* パーサの説明


まずはRuby のパーサについて説明をされました。
Ruby には1.8系列と1.9系列がありますが、パーサはparse.yで1.8・1.9共通であり、評価器(Evaluator)は1.8系列はeval.c・1.9系列はYARVになりました。ここでRuby の「秘伝のタレのようなもの」としてparse.yとeval.cがあることを話されました。
そして、読み込んだソースファイルの構文解析をするため、parse.yは2つの部分に分けられ、

* 字句解析(Lexer)
  * ソースプログラムを字句の並び(トークン)に分割する処理
* 構文解析 (狭義のParser)
  * トークンの並びから、解析木を構築する処理


があることを解説されました。

##### 実装の実演

1. ハッシュのリテラルを =&gt; から :) に変更する


実装の実演の第一弾はハッシュのリテラルを =&gt; から :) に変更するものでした。
まずはRuby の5種類ぐらいの : の使い方を説明されました。
次に、parse.yの

* 字句解析をしている部分で来た文字によって場合を分ける
* 文字の先の状態に応じて遷移先を変える


について説明をされました。

Ruby 1.9.2をビルドして動作確認されました。無事に動いて参加者の皆さんから「おー」という声が上がりました。

1. Lisp Like Symbolを実装する


次はRuby のシンボル : をLisp Likeなシンボル ' に変更してみようといったものでした。

* ' が来たときにある条件ならば状態をシンボルの開始とし、
* 対応する ' が来たら文字列、なければシンボルとする


という方針で、QuickHackな実装をされていました。
これもRuby 1.9.2をビルドして動作確認をして。無事動くことを確認されました。
「超便利」と仰っていて場内大受けでした。

1. ++iを実装する


まず、++iはi.succの略記であるとの考えから、トークンに構文を追加されました。
但し、i++のような後置演算子は実装が難しいらしいです。

1. def A#bのようなものを書けるようにしたい。


Ruby の説明で、クラスAのインスタンスメソッドbをA#bと書いたりしますが、本当にそのようにインスタンスメソッドを書けるようにすることを目指しました。

##### 参考図書について

参考図書はやはり「Ruby ソースコード完全解説」でした。

#### 感想

一般的というより逸般的というべき内容で、いかにもujihisaさんらしい楽しい発表でした。
プログラミング言語の内部を探るために、ソースコードを読むというのは大変だと思いますが、中身を理解するにはこれが一番であることを納得させられた発表でした。
パーサをいじるとお得！アメリカでもすごい人と思われるとの発言は説得力のあるお話でした。

#### 発表資料

第38回Ruby 関西勉強会の発表資料ですが、内容はほぼ同じです。以下のURLをご参照ください。
[第38回Ruby 関西勉強会の資料](http://www.slideshare.net/ujihisa/hacking-parsey-rubykansai38)

### Lightning Talks

#### 参加者数

* 発表者の豪華さがお客を呼び込んだのでしょうか？部屋の中は始まる前からいっぱいでした。最終的には立ち見が出るぐらいでした。


#### Ruby で始めるGTD

##### 発表者

* Sixeight さん


##### 発表内容

まずはSixeightさんの「Ruby で始めるGTD」から始まりました。
GTDとはDavid Allenのベストセラーである「Getting Things Done」の頭文字を取ったものだそうです。「ストレスフリーの整理術」という邦題で訳本も出版されています。

まずはこのGTDですが、

1. To doリストの収集
1. To doリストの整理
1. To doリストの実行


という手順をくるくる回す手法だそうで、これは なにかに似ていると考えたところ「テスト駆動開発」似ていると気づかれたそうです。
すなわち、

* 収集→テストを書く
* 整理→コードを書く
* 実行→テストコードを実行


だそうです。

この仕事術を実行するためにMac OS Xで動くPIMツールであるChandlerを使っていらっしゃったそうですが、新しいMac OS XであるSnow Leopardが出たときに動かなくなったそうです。

そこで替わりのPIMツールとしてSnow Leopardで動くThingsを使い始めたそうです。なかなか使いやすいツールだったそうですが、Mac OS XとLinux間のファイルの同期が上手いかないのが不満だったそうです。

そこで同期を取るためのツールとしてRuby を用いたEverythingというライブラリを作成されたそうです。
但しいくつかの不具合が残っているのと、まだデータの参照しか出来ないそうです。

##### 発表資料

[Ruby で始めるGTD](http://www.slideshare.net/Sixeight/rubygtd)

#### visualizing and processing

##### 発表者

* kyara さん


##### 発表内容

ruby-processingの使い方について説明をされました。

* processingとは


視覚的なプログラミングの基本の学習用のプログラミング言語だそうです。他の言語からも結構簡単に呼び出せるようになっているようです。

* ruby-processingとは


オリジナルのRuby からprocessingを操作するためのライブラリだそうです。
これを用いて簡単にGUIのプログラムを書けることをライブコーディングで行っていただきました。
今回は

* 日本地図を読み込んで3dで表示
* 県庁所在地を表示して線で結ぶ


といった画像処理が簡単にできることの紹介をされていました。

#### Lang-8におけるRuby 活用の一端

##### 発表者

* 松本一輝さん


##### 発表内容

松本さんご自身が開発されている語学学習用SNS　Lang-8(ランゲート)での高速化についてお話されました。

まず今までのLang-8の問題点として、アクセス速度が遅いという問題があったそうです。
これは従来のキャッシングの手法が使えないのが原因だそうです。
これに対処するためにKey-Value Store(KVS)を用いてメモリ上にデータを持つことにされたそうです。
このためにKVS実現のためのインターフェースライブラリSimpleResourceをRuby で実装され、これを用いてLang-8の高速化を図られたそうです。

ここで全てのデータは1300万ものレコードを一つのテーブルに保存し、オンメモリで読み込むようにして高速化を実現されたそうです。

* Lang-8のデータベース使用容量
  * 以前の4.0GBからMySQLの圧縮機能を使って2.1GBまで圧縮
* CPU負荷
  * 1/4に低減された


そうです。

Webアプリケーションでの最先端の技術の威力を教えていただいた気がしました。

##### 発表資料

[Lang-8でSimpleResourceを全面的に採用した件](http://d.hatena.ne.jp/kazuk_i/20091109/1257776856)

#### Web3.0

##### 発表者

* ストヤン ジェコフさん


##### 発表内容

* 今まで
  * RSSをブログなどで発行して、これをRSSリーダが巡回して変更があれば知らせるという形で情報を知らせていた
* 現在
  * Twitterが出てきたので、このような手法が使えなくなった


と前置きされ、その対処方法についてお話しされました。

ここで、RSSをRSSリーダが巡回して変更を知る。すなわちpollingの手法が問題であり、これに対処するためのRSSをサーバにpushする手法が必要であると話されました。

* HTTPを用いたpushの方法


HTTPを使ってpushは可能かという問いにはWebHooksを使えば良いと言うことでした。
WebHooksを使うとHTTPを使うので、今まで蓄積したシステムを有効活用できるので、簡単にシステムを構築できるそうです。

* 問題点
  * 標準化されていないので、パラメーターに来るデータはいろいろな種類のもの(XML・JSON etc)があること
  * セキュリティーが難しい


の2つだそうです。

* おすすめなもの
  * Watercoolr
  * PubSubHubbub


* WebHooks以外の方法は無いのか


XMPPを使えば良いそうです。今ではGoogle Waveでも使われているそうです。

これを使ったRuby のライブラリ(collecta-xmpp)をストヤンさんが既に書かれているそうです。

#### 日本Ruby の会第6期の活動について

##### 発表者

* 角谷信太郎さん


##### 発表内容

* 日本Ruby の会について
  * Ruby の開発者・使用者の支援を目的とする任意団体
* 日本Ruby の会の活動
  * Ruby リファレンスマニュアルの作成
  * るりまの発行
  * Ruby Kagiの主催
  * 地域Ruby Kagiの開催支援


「Ruby リファレンスマニュアル」と「るりま」については皆さん読んでどんどんフォローしてくださいと呼びかけていらっしゃいました。

* 特報


Ruby Kaigi2010が来年の8月27・28・29の3日間に亘って開催されることが報告されました。
開催場所はRuby Kaigi2008と同じつくばの会場で開催されるそうです。

Ruby Kaigi2010のWebサイトをLT中に作成されました。

いきなり会長から会場ちゃんと押さえているのかと質問が飛んで、「ここで決めているのかよ！」かけ声が飛んだりして、場内爆笑でした。

* 日本Ruby の会の構成


かずひこさんが理事を抜けられて、札幌の島田さんが新たに理事として任命されたことが発表されました。

* 日本Ruby の会からのお願い
  * とにかく人不足


いつも手を動かしている人たち以外の人もどんどん参加して協力して欲しい(特にるりま)とお願いされていました。

#### それMiyakoで(ry

##### 発表者

* サイロス誠さん


##### 発表内容

10/9に発表されたゲームライブラリMiyakoのver2.1についての説明をされました。

* 新機能のポイント
  * 多様なスプライトの描画方法
  * スプライトのみの配列を作れるようになった
  * 自動化の拡充


* インストール方法
  * 超簡単。gem2行だけ。


* 特報
  * 今年中にMiyakoの本が出る予定。原稿は既にできあがっているそうです。


スプライト関係がかなり充実してきたという印象を受けました。
床に座り込んでWiiリモコンでプレゼンソフトを操作するというユニークなスタイルのプレゼンでした。
出版されるMiyakoの本の内容が楽しみになるプレゼンでした。

#### 以下は飛び込みの発表

#### Ruby で楽しく開発

##### 発表者

* jugyoさん
  * termtterを開発した人


##### 発表内容

Ruby で楽しく開発するための便利なツールを2つ紹介されました。

* ifchanged
  * ファイルの変更を監視して何かをするツール
  * 例…ソースが変更したらテストを実行する
  * 監視するファイルはワイルドカードも指定できる


* g
  * pみたいなもの。オブジェクトの情報をgrowlに出力してくれる


いきなりの発表で中々面白かったです。ifchanged・g共に使ってみたいなと思えるツールでした。

#### why Ruby

##### 発表者

* yharaさん


##### 発表内容

* いきなり2つ


* why Ruby
* ホワイ・ザ・ラッキースティフ(why the lucky stiff)が8月に謎の失踪
* コードはwhy mirrorという名前でgithubにミラーが有るので大丈夫


* Ruby Staionの話
* ブラウザをデスクトップアプリのGUIにする
* 詳しくはRuby Staionで検索してください


とのことでした。

いきなり会場でお願いしたにもかかわらず、快く引き受けて面白いLTをしていただきました。

### 初級者向けレッスン(その1)・(その2)

#### 参加者数

* 定員16名なのですが、2回とも定員以上の数の方が参加されて、一部パソコンを使用できなかった人が出てきてしましました。


#### 講師

* okkezさん


#### 発表内容

とにかく参加者にRuby を実際に触ってもらおうということで、PCが使える教室で、Linuxが起動するCD-ROMを使って、実際にRuby のコードを書いてもらいました。
レッスンの趣旨は、スタックをつくろう！というお題で、スタッククラスを作りながら、テスト駆動開発のさわりを理解してもらうことになりました。
普段の勉強会では90分ですが、今回は50分と短いこともあり、okkezさんが前でスタックの簡単な説明を行った後、プロジェクタに映し出されたコードを実際にPCで動かして、動作確認をしていただくという形式を取りました。
初級者向けレッスンにはTAと呼ばれるスタッフがいます。TAは参加者を回って質問に答えるという形で、細かいことを教えることになっています。スタッフが参加者の周りを回って、手が止まっていそうな人に声をかけて教えていくという形をとりました。

#### 感想

テスト駆動開発の趣旨は中々理解されにくいものですが、今回はプログラミングのお題はスタックという非常に簡単なものに絞り、とにかくテスト駆動開発とはどういうものかを理解していただくというokkezさんのアイデアが実り、かなりの参加者にテスト駆動開発の良さについて認識が深まったと思います。
PCルームの定員と時間が少なかったのですが、参加者の人にとって有意義な講義になったと思いました。

### Ruby によるMac OS Xデスクトップアプリケーション開発入門 Snow Leopard対応版

#### 参加者数

始まる前から部屋の定員を超えて、すごい人気でした。

#### 発表者

* 高尾宏治さん


#### 発表内容

##### Ruby とMac OS Xとの関連

まずRuby とMac OS Xとの関連を時間軸に沿って説明されました。
特に2007年にRails がRuby のライブラリの一つとして標準搭載されたことについて非常に大きなチャレンジだと仰っていました。
あと感想として海外のRuby istは最近Macユーザー率が非常に高いのではないかと述べられていました。

##### Ruby でのMac OS Xでのデスクトップアプリケーション開発について

高尾さんは元々Linuxで開発を行っていらっしゃったので、殆どのMacの操作がGUIで行うのが印象深かったそうです。
公式開発言語はObjetcit-Cですが、Ruby が理解できていればObjective-Cの理解は難しくないそうです。
Ruby でのMac OS Xでのデスクトップアプリケーション開発では

* Ruby Cocoa
* MacRuby


の2つ方法があり、これから開発をしたい人にはMacRuby がお勧めだそうです。

* Ruby Cocoa
  * Ruby とObjective-Cの橋渡しを行うライブラリ


* MacRuby
  * Macに特化したRuby の処理系
  * CRuby 1.9ベース
  * LLVMで再実装されたVM　Ruby スクリプトをコンパイル可能


##### MacRuby の説明

今回はMacRuby について語っていただきました。
例として、簡単な文字列表示のダイアログボックスを作成するデモをされました。
attr_accessorにGUI部品と接続するためのインタンス変数を定義する。
(デモではtextField)
GUI部品を押したときの処理は、メソッド定義でsenderを引数にして
textFieldに文字列を代入する。
これだけで簡単に文字列を表示するダイアログボックスが作成されました。簡単な例ですが、いくつかの約束を守るだけで簡単にGUIのプログラムが作成されたのが印象的でした。

##### Mac OS X 10.6のGCD(Grand Central Dispatch)の説明

Mac OS X 10.6(Snow Leopard)の新機能であるGCD(Grand Central Dispatch)の説明をされました。
GCDとはMac OS Xで並列処理を行うためのライブラリで、現在FreeBSDにも移植が開始されているようです。

説明としては並列したい処理の部分に
Dispatch::Queue.concurrentで定義されているapplyメソッドで包めば、その部分がディスパッチキューに登録されて並列処理されるようです。
並列処理ロックの部分もきわめて簡単で、1・2行付け加えるだけで、並列処理ができるのは驚きでした。

#### 感想

Mac OS Xでのデスクトップアプリケーション作成や並列処理といった部分は中々資料がなかったので、非常に興味深い発表になっていました。
2つの話題に共通したことですが、とにかく簡潔にMacのプログラムが書けるということで、これだけでも一度使ってみたいと思う内容でした。

#### 発表資料

発表資料は以下のURLをご参照ください。
[高尾宏治日記 on はてな](http://d.hatena.ne.jp/kouji0625/20091108)

### GC 黄金時代

#### 参加者数

最初は 30 人ぐらいでしたが、最終的にはほぼ満員になりました。

#### 発表者

* nari さん


#### 発表内容

最初に簡単に自己紹介をされたあと、出席者に以下の質問をされました。

GC って何って人は挙手してください
: 1 人

GC が好きな人は挙手してください
: 5 人

GC のコード書いた or 読んだ人は挙手してください
: 4 人

##### GC の説明

「メモリ中を観察して勝手にゴミを集めて捨てにいくもの」と説明され、
「地味だけど気になる存在」と話されていました。

##### 現在の GC の実装の種類

実装方法としては 3 つに分類されるようです。

* 参照カウント
* トレーシング GC
  * マークスイープ GC
  * コピー GC


これらのメリットデメリットについて説明されました。
実装として多いのは参照カウント＋マークスイープ GC だそうです。

ここでどのオブジェクトが GC の対象になるかの見分ける方法として、2 つあることを説明されました。

* 保守的 GC
* 正確な GC


Ruby はマークスイープ＆保守的 GC で実装されているそうです。
世の中で保守的 GC で実装された言語は少数派だそうです。

##### GC の黄金時代について

黄金時代は 60 年代初頭だそうです。というわけで、現在は基礎となる理論を元に実装を改良している時期だそうです。

結論としては

* GC のアルゴリズム的な黄金時代は過ぎ去った
* 実装的な黄金時代はこれからだ！


だそうです。

##### GC の未来について

これからの GC の実装については

* 高速なストレージ (SSD) に合った GC の実装
* さまざまな並列化(CPU・言語)に合った GC の実装
* ハードウェアが GC をサポート


が出てくると予想されました。

#### 感想

低レベルなレイヤーを扱う部分なので、勉強する機会が少なく、理解の難しい話題ですが、非常にわかり易く説明していただきました。
60 年代初頭には既に理論的な基礎が出来上がっていたこと、それを始めて発表したのが、Lisp の作者でもある、John MacCarthy なのは興味深い話でした。
NaCl の紹介のときに、「GC に詳しい人がいる」のスライドでまつもとさんが出てきたときには大受けでした。

#### 発表資料

発表資料は以下の URL をご参照ください。
[GC 黄金時代](http://www.slideshare.net/authorNari/gc-2447192)

