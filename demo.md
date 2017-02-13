LPなどの視覚的なデザインを売りとしたサイトの場合、高い水準でカンプ通りの実装が求められる。自分では狂いなく再現したつもりでも、どこかでずれていてデザイナーから指摘されることもしばしばある。この記事では、[^1]デザインカンプの徹底再現（[^2] ピクセルパーフェクト）の必要性と、そのための便利なMacOSXアプリケーションを紹介する。

**要約**

* 他人の作ったデザインを高いレベルで再現するには、ピクセルパーフェクトを狙うくらいの意気込みが必要
* その為には、ブラウザへカンプを重ね合わせるチェックが有効
* Helium/Mapture/LayxerXは、フローティングと透過機能を持った非常に便利なアプリケーション

[^1]: 当記事における「ピクセルパーフェクト」とは、Webブラウザ上での表示とデザインカンプが完全に一致している状態を指す
[^2]: 当記事における「デザインカンプ」とは、Webサイト完成時の理想的な外観表示を、画像として作成した資料を指す

# なぜピクセルパーフェクトを目指すのか

Webサイトという技術の特性上、フォントが違ったり、組版の仕様が違ったり、文字サイズのデフォルト値が違ったり、モニタの色見が周辺環境や端末スペックによって違ったりとするため、**ピクセルパーフェクトにこだわる理由は本来的には無い**。

しかし、**デザイナーと実装担当者が分かれている場合、適当な意識での実装では、元々のデザインの意図を表現しきれないものができてしまう可能性がある**。これにはデザインを売り物にする上で大きな問題があるし、結局はデザイナー側から細かい修正を依頼され、予想外の工数をかけてしまうリスクもある。

他人の作ったデザインを細かいところまで再現するのは、熟練者でも簡単なことではない。ピクセルパーフェクトを狙うくらいの意気込みがあって、ようやくスムーズに実装ができるのではないだろうか。

### 重ね合わせチェック

Webブラウザ(最も再現度が高くなると想定したもの)にデザインカンプを重ねることで、高い精度で誤差を修正できる。ただし、スクショを撮ってPhotoshopで重ね合わせるのは面倒で効率が悪く、おすすめできない。

代わりに、半透明でフローティング(常にどのアプリケーションよりも最前面に表示される)機能を持った、補助的なアプリケーションの導入を薦めたい。これを使うと、**IDEでコーディングをしながら、コーディング中のサイトとデザインカンプの誤差をリアルタイムで確認できる。**

はじめからページ全体で重ね合わせをすると誤差が大きすぎるので、

* パーツ単位 ＜ モジュール単位 ＜ モジュール同士の間隔 ＜ ページ全体

という風に、小さい部分から頻繁に重ね合わせチェックをするのが良いかもしれない。面倒そうに思えるが、後述のHeliumとMaptureを使うと簡単に行える。

![MaptureとHeliumによる開発の様子をキャプチャしたスクリーンショット画像](https://qiita-image-store.s3.amazonaws.com/0/48238/cbec0dab-e85c-bc2b-c950-842996d4d73e.png)

画像はIDEにカンプとブラウザを透過で重ねている図。一見使い難そうに見えるが、邪魔な時は透明度を上げたり、掴んで画面外に置けば良く、それほど不便さはない

# 徹底再現に便利なアプリケーション

## Helium

[![スクリーンショット 2016-05-26 22.06.21.png](https://qiita-image-store.s3.amazonaws.com/0/48238/fd21558d-7b90-53ff-1cf7-875eb098fad5.png)](http://heliumfloats.com/)

* [Helium by JadenGeller](http://heliumfloats.com/)
* [JadenGeller/Helium: A floating browser window for OS X](https://github.com/JadenGeller/Helium)

任意のWebページをフローティングで透過表示できる。オプションでマウスオーバー時にだけ透過を解除したり、透過中はマウス操作を無視させることもできる。無料ソフト。

### 機能

* 任意のWebサイトを表示し、フローティング表示できる
* オプションで透明度を自由に変更できる
* マウスオーバー時にだけ透明度を変えることができる
* 透過中はユーザーのマウス入力を無視させることができる

### 便利な使い方

* 後述のBrowsersyncで立ち上げたローカルサーバを表示させ、常にコードのプレビューをIDEの上に浮かせておく

## Mapture

[![スクリーンショット 2016-05-26 22.09.52.png](https://qiita-image-store.s3.amazonaws.com/0/48238/266924f0-40e4-75d7-cdee-79a622f518fc.png)](http://anatoo.jp/mapture/)

* [Mapture - MacOSX向けキャプチャユーティリティ](http://anatoo.jp/mapture/)
* [Mac用の作業支援キャプチャツール、Maptureがいい感じになった - id:anatooのブログ](http://blog.anatoo.jp/entry/20140108/1389107218)

Windowsの[Rapture](http://www.geocities.jp/knystd/rapture.html)のように、使い捨てのスクリーンショットを手軽に作成して画面に浮かべることができる。無料ソフト。

### 機能

* 画面の特定エリアを切り抜いて画像メモ化できる
* 任意の表示倍率で、画像メモをフローティング表示できる
* スクロールホイールで透明度を自由に変更できる
* ユーザーが明示しない限り画像ファイルは保存されない

### 便利な使い方

* PSDからパーツ単位でキャプチャを取り、IDEの上に浮かべる
* Webブラウザの上に半透明で重ね、透明度をホイールでスクラブしながら、実装とカンプの誤差を確認する

## Adobe CC Extract

![Adobe CC Extract](https://qiita-image-store.s3.amazonaws.com/0/48238/01246c97-3c8c-0bd1-89b4-b6c1341687ca.png)

* [PSD 変換 - HTML、CSS | Creative Cloud Extract](http://www.adobe.com/jp/creativecloud/extract.html)
* [Creative Cloud ヘルプ | Extract による PSD から Web への抽出ワークフロー](https://helpx.adobe.com/jp/creative-cloud/help/extract-css-images-psd-files.html)

**[2016年6月28日に一旦終了した後、ユーザーの声で8月に再開](https://liginc.co.jp/301585)**を果たしたAdobeのフロントエンドエンジニア向けのWebサービス。AdobeCCで利用できるサービスに含まれる。

CreativeCloudのオンラインストレージにアップロードしたPSDデータを解析し、**Webブラウザ上で横幅・高さ・フォントサイズ・行高などを即座にCSSコードとして取得したり、特定のレイヤー画像から画像を抽出・ダウンロードすることができる。**

![スクリーンショット_2016-09-07_21_46_09.png](https://qiita-image-store.s3.amazonaws.com/0/48238/355b2899-a29c-66d9-c07b-a8cf19ee08f3.png) ![スクリーンショット_2016-09-07_21_46_25.png](https://qiita-image-store.s3.amazonaws.com/0/48238/b2fe10a6-385e-2183-c85c-4ac1415f82fa.png)

 ![スクリーンショット_2016-09-07_21_46_45.png](https://qiita-image-store.s3.amazonaws.com/0/48238/da531e30-14b0-a666-640f-19a904185980.png)

UIが非常に使いやすく、**マークアップ担当者にとって必要な作業はがほとんどWebブラウザだけで完結する**。余計な機能がないので、むしろPhotoshopよりも使いやすい。既にAdobeCCアカウントを持っているのであれば、是非使ってみたいサービスだと思う。

### 機能

* レイヤー情報からのCSSコードの出力
* レイヤーからの画像出力(PNG・JPEG・SVGなど)
* レイヤー間の隙間の計測
* レイヤーの表示切り替え
* ファイルのオンライン共有
* PSDデータの実寸表示〜拡大・縮小
* フォント・カラー値の抽出

### 便利な使い方

* マシンリソース節約

## LayerX

[![スクリーンショット 2016-05-26 22.11.07.png](https://qiita-image-store.s3.amazonaws.com/0/48238/65a71e77-f861-6b2e-a6a1-127e2f22d6bf.png)](http://yuhua-chen.github.io/LayerX/)

* [LayerX - An intuitive app to display transparent images on screen.](http://yuhua-chen.github.io/LayerX/)

任意の画像ファイルをフローティング表示できる。細かいレイヤーの切り替えはできないが、PSDを直接表示することも可能。無料ソフト。

### 機能

* OSXが対応する標準的な画像形式のファイルに対応
* 任意の表示倍率で、画像をフローティング表示できる
* スクロールホイールで透明度を自由に変更できる
* 「ロック」ボタンを押すと位置と透明度が固定され、マウスクリックを無視する状態にできる

### 便利な使い方

* PSDファイルを薄めに透過させて、ロック状態でIDEに重ねる

## xScope

![スクリーンショット 2016-05-26 22.27.52.png](https://qiita-image-store.s3.amazonaws.com/0/48238/6d91a724-9bd1-c65d-c469-bbc2fbd43c8a.png)

* [xScope • Measure. Inspect. Test.](http://xscopeapp.com/)

定規・ガイド・モバイル端末へのミラーリングなど、スクリーン上のピクセルの測定や解析に特化した強力なツール。49.99ドルの有料ソフト。

### 機能

* 自動でマウスポインタ近くのエリアを測定する「Dimension」ツール
* マウスポインタを中心に座標とX/Yガイドを表示する「Crosshair」ツール
* 画面全体にX/Y軸ガイドを自由に設置できる「Guides」ツール
* [ほか多数](http://xscopeapp.com/guide)

## Browsersync

[![スクリーンショット 2016-05-26 22.47.07.png](https://qiita-image-store.s3.amazonaws.com/0/48238/df9e664e-4c8b-5291-0552-39572011312b.png)](https://www.browsersync.io/)

* [Browsersync - Time-saving synchronised browser testing](https://www.browsersync.io/)

node.jsによるオートリロード機能のある開発用Webサーバ。無料ソフト。

オートリロードがないとHeliumの導入効果が低下してしまう。node.jsやgulpとセットで環境を作る必要があるが、まだ導入していない場合はぜひ使用を推奨したい。

* [ブラウザ確認が一瞬！ Grunt・Gulpと始めるBrowserSync入門 - ICS MEDIA](https://ics.media/entry/3405)

---

