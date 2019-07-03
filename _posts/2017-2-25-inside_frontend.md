---
layout: post
title: Inside Frontend #1
---

# 開催概要
+ 日時：2017/2/25(土)
+ 場所：Yahoo! JAPAN＠東京ガーデンテラス紀尾井町
+ URL：[Inside Frontend](http://inside-frontend.com/){:target="_blank"}

---
## Webフロントエンドにおけるコンポーネント化のアプローチ
[発表スライド（スピーカーのブログ）](https://1000ch.net/posts/2017/component-of-web-frontend.html){:target="_blank"}

+ Sensui Shogo氏（Cyber Agent Inc.）

### 少し前のWebにおけるコンポーネント化の話題
+ スタイルガイド
+ プロジェクトUIのドキュメントして
	+ フロントエンドエンジニアがコピペして使うためのドキュメント
	+ メンテナンスされない
+ 何を解決すればいいのか本質的に見えていなかった


### コンポーネントの利点
+ コンポーネント＝特定の機能、特に再利用を考えて部品化したもの
+ UIの一貫性・汎用性を考えたもの
+ 機能におけるアフォーダンス
+ Webクライアントサイドにおけるコンポーネントは最終成果物の勝ちを左右し得るもの
+ ボタンやラベルの見た目・挙動を統一化するため

### 管理手段の問題
+ デザイナとスタイルガイドうまく共有できている？
	+ デザインデータの更新?スタイルガイドの更新

### 誰が管理する問題
+ スタイルガイドがエンジニアの持ち物だということが問題
+ コンポーネント設計はWebに依存しない
+ コンポーネントドリブンの考え方をエンジニアしか持っていなかったことが問題

### 解決策
+ コンポーネント単位で分割するのが重要
+ デザイナが継続してメンテナンスできる
+ Sketch Import Symbols
	+ 1つのSketchファイルから外部のScketchファイルを参照できるので、コンポーネントのマスタファイルから参照してデザインデータを管理できる
	+ フォトショなら可能

+ 協働のためのデザイン思考の再構築（HTML5Conの資料）
	+ デザイナは全体からディティールを詰める
	+ エンジニアは部品から全体を作る
+ 開発プロセス上の必然ついて
	+ 全体像の表現化課せられるデザイナ
	+ 実装の前提であり、実装の依存が強い
	+ デザイナとエンジニアの歩み寄りが必要。デザイナは実装を理解し、エンジニアはデザインを理解せよ

### コンポーネント化を実現する上での技術的課題
+ CSSはスコープがなく脆く壊れやすい言語
	+ 可搬性がない
		+ いかに優れたコンポーネント設計でも上書きを防げない
	+ CSS設計は最低限のスパゲティ対策にすぎない
+ CSSは設計を工夫してもデザイン次第で破綻する
	+ とはいえスコープは欲しい
		+ CSS Modules
		+ CSS in JS
+ Shadow DOM
	+ スコープの実現：要素単位のスコープを定義、再配布可能な本来のコンポーネントの実現
	+ Custom Elementsによる要素の再定義：任意のUIや振る舞いをまとめられる、Web Components

### 協業実践に向けた方針
+ 職能同士の歩み寄り at 現場
	+ 開発上・品質上のメリットの提示（not エンジニア都合）
		+ 説得材料の交換（エンジニア, デザイナ）
	+ お互いの作業を小さく分担
		+ 予期される振る舞いをエンジニアがレビューする
		+ UIの表現部分をデザイナが実装する
+ トップダウンな話
	 + ステークホルダとの合意形成
+ ボトムアップな話
	+ 現場手動の草の根活動＝根気が問われる
		+ 開発プロセス化することでの定着
	+ フレームワークの導入
		+ Atomic Design（Abema TVでも導入）
			+ 成功事例の共有
+ 識者に学ぶ

## 実録、アメブロリニューアル2016
[発表スライド](https://speakerdeck.com/herablog/ameburo-2016-shi-lu-ameburoriniyuaru275ri-webpahuomansubian
){:target="_blank"}

+ Kazunari Hara氏（Cyber Agent Inc.）

### アメブロリニューアル？
+ システムのリプレースのプロジェクト
	+ 45,248行書き換えた
+ IsomorphocなWebで成果
	+ Webパフォーマンスの向上、直帰率↓
+ 採用技術はReact, node.js, docker,などなど
+ リポジトリはGithub

## Plan
+ プランニングはGistにメモ程度に書く
	+ 業界標準のものを使いたい＝大きな開発Communityがある
+ Frontend Server：Nodejs
	+ 社内の実績・知見がある
+ JS
	+ React, Redux, ES6, ESLint（厳し目に入れたのでCircleCI通らない人も）
+ CSS
	+ PostCSS, CSS Modules（ReactのComponentと対にして管理）
+ Style guide
+ Webサービスを利用。実験段階。（詳しくはSlideShareで）
+ モダンなMETA（refs slideshare）
+ アクセシビリティ（refs WAI-ARIA　状態をマシンに伝える）
+ AMP（refs アメブロにおけるAMP）
+ Build
	+ Gulp→Webpack, packag.json
+ パフォーマンス
	+ HTTPのリダイレクトを避ける
	+ ローディングのブロッキングをやめる
	+ 最初に必要なものはインラインで書く
	+ 初期表示に必要ないものはあとから呼び出す
		+ 自分たちで調査・課題設定して継続することが大切
	+ SpeedCurveで解析したところ、初期表示も最終読み込みも遅い
		+ 表示速度2倍を目標に設定して実施
	+ メインコンテンツ以外はLazy Loadするようにした
+ Modern Workflow
	+ git-flow, PullReqest
	+ CIによる自動テストビルドデブロイ
	+ 新しく入ってきた人が何をしたらいいのかわからなくならないように、Readmeを整備した

### DO
+ パフォーマンスの向上
	+ SSR+Lazy Load
	+ Webpackでbundle
	+ いらない読み込みの削除
		+ コードを読んでリストアップ
	+ 画像のCSS化
	+ No more ガタンッ
		+ 読み込んでからコンポーネントの高さが変わっていて、誤タップが多かった

### 負荷試験
+ 過去のアクセスログを元に検証
+ 10,000rpsで試験
+ New Relicを使用
+ DockerのモニタリングにはDATADOGを使った
+ 結果は悪かった→使い物にならない

### チューニング
+ node --inspect index.js
	+ inspectオプションをつけることでChromeで検証できる
+ RenderToString()が遅かった（いまは有名な話だが、当時知られていなかった）
	+ キャッシュの利用をした。静的ドキュメントが多いのでキャッシュ効率がいい（73.66%）。
+ 開発サーバ
	+ Redisを使っていたが、相性が悪かった
	+ Memcachedのほうが、データ量大・高アクセス時のときはよい
+ 複数のcontainerを1つのProxy（HAPROXY）で見ていたが、パフォーマンスがよかったが、それぞれのHost付けにしてProxyを立てるようにした

### リリース
+ 段階リリースうまくいかない
+ Slackに知らない人が入ってくる
+ 段階リリースうまくいかない
+ Slackにエライ人が入ってくる

### One more things
+ Front-end Performance checklist 2017
	+ HTTP2を取り入れたい
+ Lighthouse
+ 老害にならないようにがんばらないといけない

---

## karmaを使ったSPA向けのE2Eテスト技法

+ @kyo_ago氏（Chatwork）

### 謝罪
+ E2Eと銘打っているが、インテグレーションテストといったほうが適切だった

### 今回伝えたいこと
+ SPAのテストにWebDriverは向かない

### Webdriverとは
+ Seleniumから発展したツール
+ 歴史あるE2Eテストの鉄板ツール

### なぜ向かないのか
+ あくまでも画面を遷移していくWebサイトのためのテストツール
+ DeveloperTool上でできることがWebDriverだとできないことがある
	+ Node contextとBrowser contextが分断されている
+ DriverによってはDevelopper Toolsと競合する（Chromeなど）
+ console.logの内容がterminalでしか確認できない
	+ Objectの中身が展開できない
+ ページの読み込みやクリック後の遷移を待ってくれる機能がある
	+ SPAは画面遷移をしないので、JSのハンドラを検知したかどうかは大切ではない
+ SPAのインテグレーションテストにはKarmaがおすすめ

### karma?
+ 社内で話をしたところ「あれ、AngularJS専用ですよね？」「Protactorになったから終わったと思ってました」との声
	+ まだまだ開発は活発（5日前に
	+ ProtractorはWebdriver系のツールなので別物
+ ブラウザ上でテストが動く
+ まるでサイト上でユニットテストを走らせているかのように書ける
+ 読み込みがlocalhostで行われる
	+ 実際にテストしたいドメインで読み込まれるわけではない
+ 別ドメインに通信したい
	+ 1.通信の書き換え：Local Proxyを使う　$ npm install karma-proxy-plugin
	+ 2.通信の向き先の変更
+ develop toolのConsole上で検証しているような手軽さ

### つらいところ
+ ブラウザ起因の不安定さがある
+ 状態のクリアが自分の責任になるので辛い
	+ 自分で制御できるレベルが上がるのは嬉しい

+ Webdriverは受け入れのテストツールであって、開発向けのテストツールではない
+ Webdriverは高性能だけど、不要な機能も多い

### E2Eテストとは
+ End to End
	+ 対象範囲の話
	+ 「開発のために」「検証のために」目的によって使い方は変わる

### QA
+ Browserstack とか soucelab は高い割に有用なテスティングができているのか不安。どう解消すればよいか
	+ サービスに依存していると、向こうのサーバが落ちるとテスティングできないのはつらい。travisCI上でテストをしている
	+ クロスブラウザで確認する場合は外部サービスを利用するのもやむを得ない。BrowserStackにはサービスプランもあるのでそちらを検討してみてはどうか。

---

## 雑感
+ Inside Frontendという勉強会は、今回が１回目ということでした。
	+ 初学者にも参加しやすい空気感でした。また、スピーカーもある程度は噛み砕いて話してくださるため、「何を言っているんだ…？？？」と聞いて困ることはなかったです。
	+ WiFiがあるのはもちろん、なんと電源タップも使って良いということで素晴らしい会場設備でした。
	+ AMA ブース ( Ask Me Anything )というものがありました。Yahoo!の方が用意してくださったお菓子を食べながら気軽に登壇者と話ができるというものです。今回はビビって参加しませんでしたが、ぜひ次回は現場での疑問を持って行けたらなと思います…！
+ 「Webフロントエンドにおけるコンポーネント化のアプローチ」では、スタイルガイドをデザインデータで管理するという発想が斬新で驚きました。
	+ また、協働するためにはエンジニアとデザイナの歩み寄りが大切なんだというお話を聞いて、以前から思っていたデザインの勉強をしっかりしたい、という思いが再燃しました。
	
+ どこもDockerを導入していたのでやっぱりDockerの勉強をしようと思いました。。