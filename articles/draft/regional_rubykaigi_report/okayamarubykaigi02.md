# RegionalRubyKaigi レポート岡山 Ruby 会議 02
## 開催概要
### 開催日
2013 年 07 月 06 日 (土) 10:00 〜 17:30
### 開催場所
岡山県立大学 学部共通棟（東） 8901 室
### 主催
岡山 Ruby 会議 02 実行委員会
### 後援
日本 Ruby の会, 岡山 Ruby / Ruby on Rails 勉強会
### 公式ページ
http://regional.rubykaigi.org/okayama02
### 公式ハッシュタグ
\#okark02

## はじめに
今年も無事開催することが出来ました。昨年は午後だけのイベントでしたが今年は午前からの開始でボリュームアップしての開催です。

# 一般講演
## 私と Ruby の付き合い方
### 小西雅也 (@ore\_public)
岡山 Ruby 会議の最初のセッションは Okayama.rb を主催し、るびま編集者としても活躍されている小西雅也さんです。「私と Ruby の付き合い方」というタイトルで、普段どのようなツールや開発環境を使って Ruby を楽しんでいるかを語っていただきました。

#### パソコン
普段は MacBookAir を使っているそうです。Cocoa アプリケーションが Emacs 風キーバインドになっているので使いやすいそうです。また、サウンドやカメラの設定上のトラブルが少なくハードウェアに悩まないこともポイントが高いそうです。

#### ターミナルとシェル
ターミナルは iTerm2 上で tmux を動かしているそうです。tmux は複数の画面を切り替えて使うことができる仮想ターミナルソフトですが iTerm2 で使用するとマウスでのスクロールやタブの切替に対応しており、標準のターミナルより便利に使用できます。
コマンド履歴検索機能が強力なのでシェルは zsh を利用しているとのことです。行の右側に ruby のバージョンと git のブランチ名が出るように設定していました。

#### RVM
Ruby のバージョン切り替えツールは、コンパイルに必要なパッケージも引っ張ってきてくれる RVM が気に入っているそうです。流行りの rbenv はソースから自分でコンパイルした Ruby を切り替えたりする用途に使っているとのことです。用途ごとにツールを使い分ける良い例だと思いました。

#### エディタ
色々設定すれば vim や emacs は便利に使えますが、Sublime Text はデフォルトでの配色や設定がかなり良くすぐに使えるとのことです。また IDE では RubyMine のコード補完やジャンプが充実していて cucumber の step 定義や ActiveRecord の動的メソッドにまで飛んでいってくれるそうです。初心者には参考になる情報だったのではないでしょうか。

#### デプロイ先
株式会社 paperboy&co. が運営している sqale に趣味で作成したサーバー監視サービスをデプロイしているそうです。git に push するだけでデプロイしてくれるので便利とのことです。
AWS は簡単にディスクイメージのバックアップを取って実験でききるのが魅力とのことでした。IaaS や PaaS サービスは実際使ってみないと細かい操作性が分からないのでこれからサービスを始めようと思っている人には良い情報だったと思います。

## Jenkins で行う並列テスト
### 山本和久(@kazuhisa1976)

前回の岡山 Ruby 会議に続いて、テストについてのお話を聞かせてくれる株式会社リゾームの山本さんの講演です。  
  
山本さんは 2011 年 7 月に開催された RubyKaigi 2011 に参加してテストに対する意識が高くなり、担当しているプロジェクトにテスト環境を導入して開発を行っていました。しかし、プロジェクトが進行するにつれてテストコードが膨らんでしまい、テストに時間がかかるようになってしまいました。  
  
「テストが遅いので、ローカルのマシンでテストを行うと開発の妨げになる…」。  
  
参加者たちも「よくあることだ」と思いながら傾聴していましたが、山本さんはテストが開発の妨げになることを防ぐために、次のことを始めたと話しました。  
・parallel\_tests の利用  
・Jenkins をインストールしたテスト用マシンでのテストの実行    
テストを複数のプロセスで実行する Gem である parallel\_tests を利用してテストにかかる時間を短縮させて、あらかじめ決められた処理を自動に行う Jenkins をインストールしたマシンでテストを行うことで、開発の妨げにならないようにと考えたそうです。これでしばらくは快適に開発が行えるようになりましたが、さらにプロジェクトが進行するとテストコードがもっと膨らんで、またもテストに時間がかかるようになりました。そこで、山本さんは複数マシンで並列にテストを実行することを考えました。Jenkins で並列にテストを行える運用にするには、次のことをしっかりと決めておかないといけないと話しました。  
・Jenkins のビルドパイプライン  
・テストコードの分割方法  
・開発用ブランチからリリース用ブランチに push するルール  
Jenkins のビルドパイプラインについてはデモ画面を見せながら、山本さんが取り組んできたことをわかりやすく説明しました。また「全てのテストが同時に終わるようにテストコードを分割する」「全てのテストが通っていないとリリース用ブランチに push できないようにする」と並列にテストを行うときに大事になる考えを話しました。  
  
問題に遭遇するたびに改善策を探していき、「快適に開発が行えるようにしたい」という想いが伝わってくるお話でした。Ajax のタイムラグで時々失敗してしまうテストがある問題や、複数のテストが同時に実行されてときに結果が混ざって見にくくなってしまう問題が残っているので、今後はそれらを改善したいと話しました。

## 私とRuby の3年間
### 行森奈雄(@sutorada)

「Ruby を知って、人生が変わった」。  
  
そんな発言で場を沸かせた、専門学校ビーマックス学生の行森さんの講演です。  
  
行森さんは中学生の頃に学校で Linux を触っているところを先生に見つかり、「中高生 Ruby プログラミング講座」というイベントに出てみるように勧められ、Ruby に興味を持つようになりました。それからは東京のイベントで講演をしたり、オープンスクールでプログラミング講座を開いたりと、活発に行動していたそうです。オープンスクールでは四則演算のプログラムを作る講座を開いたり、アルゴリズムについての話したり、ライブコーディングをしたり、どうすれば参加者がプログラミングに興味を持ってくれるのか考えて教えてみましたが、思うようにいかないことが多かったそうです。最近は「"まつもとさん"と言う日本人が作ったプログラミング言語だよ」と Ruby について簡単な説明をして、自分で作ったゲームを遊んでもらう方法がうまくいっていると話しました。また、このような活動を続けているうちに、家族のコンピュータに対する見方が良くなったそうです。Ruby で「日常」を変えようとしている姿は、参加者たちに大きな印象を残したでしょう。  
  
学校で長期休暇を楽しく過ごせるアプリを作る課題が出されて、Ruby でゲームを作ろうと考えていたそうですが、課題で使用する言語が Java に決められてしまったそうです。「岡山 Ruby 会議で Ruby のことを話してきた」と教授に熱意を伝えて、「日常」で Ruby が使える機会を増やしていただきたいと思います。

# 招待講演
## Rubyistによるアジャイル開発
### 川端光義(@agilekawabata)

遠路、大阪から来ていただきました。株式会社アジャイルウェアで受託開発をされている川端さんの発表です。
川端さんは元々Javaエンジニアで、アジャイル開発を実践、その経験から書籍の執筆もされたそうです。
そして使う言語がJavaからRubyに変わったときに衝撃を受け、自分はプログラマとしてまだまだひよっこだと感じたそうです。
そんなRubyで受託開発を始めて、2012年に株式会社アジャイルウェアを設立。
川端さん自信はここ1年くらいプログラミングをしておらず、経営業務と営業がメインとの事です。
本日は、Rubyistと一緒に仕事をしたというお話をしていただきました。

開発事例の紹介で、いくつかのプロジェクトの事例を発表されたのですが、どのプロジェクトも競合が居るなかで受注を獲得できた決め手は短納期や、低コストだったそうです。Rubyによる生産性の高い開発が実現出来、それが武器になっているんだなと感じました。
また、開発の生産性が高まると色々な変化が出たそうです。

- 開発プロセスが変わる

ドキュメントをほとんど作らない。納品物としても作らない。ドキュメントを作成・修正して意識合わせするよりプログラムを作成・修正して意識合わせする方が早い。まさにプログラミングが要件定義そのものとなったとのことです。

- コミュニケーションが変わる

上記のようなスタイルで開発を進めているので要件を細かく伝えなくても良くなるようになったそうです。

- テストが変わる

テスト駆動開発はできない。テスト駆動しようと思うと、要件が最初に決まってないと出来ない。
細かい要件を聞かずに、ソフトウェアを作りながら、頻繁に変更も発生することからテストを最初に書いて開発するということにならないとのことです。

発表後にもたくさんの方が質問されており、Rubyでのアジャイル開発の実際の事例が参考になったかたが多いのではと感じました。

### 川端さんが執筆された本
http://www.amazon.co.jp/%E3%83%90%E3%82%B0%E3%81%8C%E3%81%AA%E3%81%84%E3%83%97%E3%83%AD%E3%82%B0%E3%83%A9%E3%83%A0%E3%81%AE%E3%81%A4%E3%81%8F%E3%82%8A%E6%96%B9-Java%E3%81%A8Eclipse%E3%81%A7%E5%AD%A6%E3%81%B6TDD%E3%83%86%E3%82%B9%E3%83%88%E9%A7%86%E5%8B%95%E9%96%8B%E7%99%BA-Be-agile-%E5%B7%9D%E7%AB%AF/dp/479810714X

## Railsアプリのセキュリティ対策入門
### 大垣 靖男(@yohgaki)

PHP界で有名な大垣さんがなんと岡山Ruby会議に登場です。セキュリティの専門家でもある大垣さんにRailsアプリのセキュリティ対策について語って頂きました。

#### 一般的なお話
Railsに限らず一般的なITセキュリティのお話をして頂きました。
ITセキュリティの3要素として機密性・完全性・可用性の3つがあげられます。これを順守するために次のサイクルを回す必要があります。

1. リスクの識別
1. 緩和策の選別
1. 緩和策の導入
1. 状態の検査
1. 1に戻る
 
よくある勘違いとして「セキュリティは完璧でなければならない」という意見がありますがリスク管理を行い、許容できるレベルまでの対策を行うことが大切とのことです。そのための指標として法律や標準、ベストプラクティスにならうことが重要です。

#### Railsアプリのセキュリティ
Webアプリの基本構造は次の3つの層に分かれます。

- 入力
- 処理
- 出力

この中でも脆弱性が起きやすいのは入力と出力です。後述のSANS/CWE TOP25 Monster Mitigationの#1と#2にも記述されています。

Rails4から採用された仕組みとしてStrong Parameterがあります。Controllerでバリデーション(※)を行うことで、Modelより入力に近い場所でチェックを行うことが可能となりました。これはModelでのバリデーションと組み合わせて使用することで「多重のセキュリティ・フェイルセーフ」になりより強固なアプリケーションを構築することができます。

#### JavaScirptインジェクション
クロスサイトスクリプティングの対策になります。 JavaScriptインジェクションは侵入経路が多岐にわたる上、クライアントで実行されると全くログに残らないため非常に厄介です。基本的にはRails標準のHelperを使うことが大切とのことです。

#### CSRFとセッション
Rails4もRails3と同様のCSRF対策が施されています。ただおかしなリクエストが来た時の挙動が変更になっているので注意が必要とのことです。

- Rails4 例外
- Rails3 セッションをリセット

またセッションIDはログイン後にreset_sessionでリセットすることが望ましいそうです。

#### 必ず参照して欲しい資料
RailsでWebアプリケーションを作る上で次のサイトを必ず参照して欲しいとのことです。
- Railsセキュリティガイド
- OWASP TOP 10
- SANS/CWE TOP 25

注
ここでのバリデーションとはRailsにおけるvalidatesメソッドが行うようなバリデーションに限らず、より広い意味の「入力チェック」の事を指しています。

# LT
一般講演の終了後に、希望者がLTを行う時間が設けられました。今回の岡山Ruby会議では9名の方が発表されました。

- 弊社とまつもとさんの関係とか地方でRubyの仕事を選択していくということ　山本由佳里  
- Ruby/PureImage　@keisuke_n  
- 関西 Ruby 会議方面から来ました！　@muryoimpl  
- lambda_driver.gem で加速する関数型プログラミング  @razon  
- mikutter を導入しよう　@kasoku_ksk  
- レガシーブラウザ対応について　@LuckOfWise  
- Okayama.rb #11 に参加してきた！　イワタ  
- RubyistのためのKotlin紹介　@patorash  
- FizzBuzzで学ぶRuby　小西雅也

## 弊社とまつもとさんの関係とか地方でRubyの仕事を選択していくということ
### 山本由佳里  
倉敷市で仕事をされている山本由佳里さんは、島根県で生まれ育った父の影響で島根県が推進しているプログラミング言語である Ruby に興味を持つようになり、書籍などで勉強されていたそうです。また、父が役員をしている株式会社システム工房エムがまつもとさんが勤務されているネットワーク応用通信研究所（NaCL）と関わりがあるそうで、Ruby により興味が持てるようになったそうです。仕事では Java を使った開発を依頼されて、「Ruby を使いたい！」と思いがあっても Ruby を使えない場面が多いそうですが、「Ruby が使いたいならば Ruby を使える仕事を待つなのではなく、自分で積極的に Ruby を使っていくのが良い。」と話されました。

## Ruby/PureImage
### @keisuke_n  
画像処理を行うライブラリである PureImage について @keisuke_n さんが発表されました。PureImage には文字やグラフの描画をはじめとする様々な機能がありますが、Rubyist にとって何よりも嬉しいと思うことは Ruby の標準ライブラリだけで作られていることです。「Ruby の標準ライブラリは適度にパフォーマンスチューニングされているので、標準ライブラリだけで作れば早い処理ができるようになる。」という考えを話し、標準ライブラリだけを使ったピュアなコードを書く方法を参加者たちに勧められました。

## 関西 Ruby 会議方面から来ました！
### @muryoimpl  
2013年8月31日に大阪で関西Ruby会議05が開催されます。@muryoimpl さんは招待講演者として Rubyist として活躍している方を呼んだことや「survive」という開催テーマについて話し、参加者たちが関西Ruby会議05に興味を持つように、楽しく宣伝されました。

## lambda_driver.gem で加速する関数型プログラミング
### @razon  
Ruby の Proc オブジェクトで関数合成や引数の入れ替えをできるようにする lambda_driver という gem を @razon さんが紹介されました。関数型プログラミングが好きな Rubyist は多いので、この gem に興味を持った方は多いのではないでしょうか。

## mikutter を導入しよう
### @kasoku_ksk  
mikutter という Ruby で書かれた Twitter クライアントを @kasoku_ksk さんが紹介されました。@kasoku_ksk さんは 「プラグインが自由に作れること」や「Ruby のコードを実行できること」などの mikutter の利点を話し、多くの人に使ってもらいたいという気持ちをアピールされました。

## レガシーブラウザ対応について
### @LuckOfWise  
レガシーブラウザに対応させるときの苦労を @LuckOfWise さんが発表されました。@LuckOfWise さんが関わっているWebアプリケーションでは、レガシーブラウザ専用のWebページを用意し、コードを分割することでレガシーブラウザに対応させたそうです。しかし、メンテナンスの手間が増えてしまうので良い方法とも言えません。@LuckOfWise さんは「レガシーブラウザ対応は断りましょう。」と話されました。

## Okayama.rb #11 に参加してきた！
### イワタ
Okayama.rb に初めて参加し、そこで感じた楽しさをイワタさんが発表されました。Okayama.rb はプログラミングが好きな人たちが岡山市のファミリーレストランに集まってワイワイ話したり、コーディングをしたりするコミュニティです。イワタさんは Ruby 初心者ですが、Ruby の開発環境を整えるところから話しを聞くことができたそうなので、「初心者でも楽しめます。」と話されました。

## RubyistのためのKotlin紹介
### @patorash  
Kotlin という JetBrains 社が開発したプログラミング言語を @patorash さんが紹介されました。Kotlin は Java の思想をベースにして作られた言語ですが、Rubyist でも読み易いコードが書けるそうです。

## FizzBuzz で学ぶ Ruby
### 小西雅也  
Ruby で FizzBuzz を実装するとき、どのような方法が良いのか調べたことを小西さんが発表されました。小西さんは Fixnum クラスに新しいメソッドを追加して FizzBuzz を実装する方法（オープンクラスによる実装方法）や、Ruby 2.0 から加わった Module#refine と main.using を使う方法を紹介されました。コードが掲載されたスライド（[http://www.slideshare.net/mkonishi1981/fizzbuzzruby](http://www.slideshare.net/mkonishi1981/fizzbuzzruby)）が SlideShare にアップロードされており、Module#refine の使い方の勉強になりますので、写経すると良いと思います。

# 懇親会
昨年と同じRyoutei 座スタジアムでの懇親会で、会場のプロジェクタを活かしてのLT大会を開催しました。
飛び入り参加OKのLT大会で、大変盛り上がった懇親会となりました。

