# お絵かき掲示板PHPスクリプト Petit Note
- 1スレッド1ログファイル形式のスレッド式の画像掲示板です。  
- PaintBBS NEO,ChickenPaint,Klecksが使えるお絵かき掲示板です。
##  動作環境
- PHP5.6以上の環境が必要です。  
PHP5.6,PHP7.2,PHP8.1で動作確認しています。  
PHP7.4～PHP8.1での使用を推奨します。

##  v0.9.16.x以前のPetit Noteをご利用の方へのお願い

## 個別スレッドのファイルの編集時にファイルロックがかかっていませんでした。
このバグによりログが破損する可能性があります。
通常は編集、または書き込みが同時に行われても一瞬でも先にファイルを開いた側が他からファイルを読み込めないようにロックします。 
そのロック処理が二箇所抜けていました。
その他の機能追加が特に必要ではない方もアップデートをお願いします。    

## v0.9.8.7.2以前のPetit Noteをご利用の方へのお願い

- テーマのHTMLの｢BASIC｣ディレクトリと、index.php、functions.php、config.php、thumbnail_gd.phpの更新が必要です。  
セキュリティリスクを回避するためアップデートをお願いします。


## ダウンロード

- [リリース](https://github.com/satopian/Petit_Note/releases/latest)から安定版をダウンロードできます。

## Peti tNoteを使った交流サイト
- [イラスト投稿サイトPetit Note](https://paintbbs.sakura.ne.jp/petit/)  
お絵かきとアップロード。
- [お絵かき掲示板交流サイトPetit Note](https://paintbbs.sakura.ne.jp/)  
お絵かきのみ。
## DEMO
- [Petit Note サンプル掲示板](https://paintbbs.sakura.ne.jp/cgi/neosample/petitnote/)  
  
![image](https://user-images.githubusercontent.com/44894014/134553433-d50e05be-a483-4b94-a575-3cead96b6720.png)

## BBSNoteやPOTI-boardのログファイルをPetit Noteで使うためのログコンバータ

- [Petit Note プラグイン](https://github.com/satopian/PetitNote_plugin)  

BBSNoteとPOTI-boardのログファイルをPetit Note形式に変換できます。  
ただし新しく設置したPetit Noteで変換したログを使う事しかできません。   
変換して新しくできたログファイルで上書きすると既存の投稿は消えてしまいますのでご注意ください。

## 履歴

## PitNoteとは
- 1スレッド1ログファイル形式のスレッド式の画像掲示板です。  
- HTML5+JavaScriptの新しいアプリPaintBBS NEO、ChickenPaint、Klecksが使えるお絵かき掲示板です。

##  22/08/16 v0.23.3

### 更新
- jQueryをv3.6.0に更新しました。
- Klecksを最新版に更新しました。  
ノイズフィルタが追加されました。
  
![image](https://user-images.githubusercontent.com/44894014/184863023-12eefd41-0ac0-4f9a-b165-235d33d533eb.png)

### 改善
-  [禁止ホストが設定できるようになりました。](https://github.com/satopian/Petit_Note/commit/d660e1e1b98131e3ed9f1089e193b55e33495ddf)

```
//禁止ホスト
$badhost =['example.com','example.org'];

```
config.phpに上記設定項目を追加する事で、指定したホストからの書き込みを拒絶できます。

- クリックジャッキングの脆弱性を修正しました。  
フレーム内に掲示板を表示しないのであれば下記設定項目の追加は必要ありません。
フレーム内で表示したい方のみ、下記設定項目をconfig.phpのどこでもいいので貼り付けて設定してください。
```
//iframe内での表示を 拒否する:true 許可する:false
//セキュリティリスクを回避するため "拒否する:true" を強く推奨。

$x_frame_options_deny=true;
// $x_frame_options_deny=false;

```

- スマホ操作に適した表示に。
- 表示高速化。JavaScriptを先読みして、クリティカルチェーンを少なく。
- ページーングのループを削減。コードを短縮。
- これまではjQueryのバージョンを変更するにはテンプレートを開いて設定を変更する必要がありました。  
jQueryのバージョンをindex.phpの設定から読み込んで、テンプレートに自動的に反映できるようにしました。
- [見えている範囲にloading="lazy"を指定しない。](https://github.com/satopian/Petit_Note/commit/5accb75dee34cba964930365c2d7a1443e560bf2)

すでに表示されているところにloading="lazy"が入っていると表示が遅くなるため、スレッドの上のほうの画像には`loading="lazy"`が付与されないようにしました。

- PaintBBS NEO起動画面の時計のJavaScriptを修正しました。  
[コンテンツセキュリティポリシーを設定したらPOTI-boardのお絵かき画面の時計が動かなくなりました。｜さとぴあ｜note](https://note.com/satopian/n/n7b757ee05975)
### バグ修正
[unixtimeが未入力でブランクの時に致命的エラーが発生していたのを修正しました。](https://github.com/satopian/Petit_Note/commit/6b6c9e17ce9c217b3eb0a18377e3ba48d5ed6b97)

##  22/07/11 v0.22.5
### 改善
- 記事の管理のための時刻を13桁から16桁へ。
マイクロ秒の下3桁を6桁に増やしました。
この変更はまったく同じ投稿時刻になる可能性を1/1000に下げるためです。
また、仮に重複しても1秒分ずらして対応できるように処理を書き直しました。
- お絵かきの投稿を管理している時刻も16桁に増やしました。
- お絵かきの投稿時にすでに同じファイル名の画像が存在している時は秒数を1秒ずらして重複を回避します。
### 更新
- Klecksを最新版に更新しました。
編集メニューにグリッドを描画するフィルタが追加されています。

##  22/06/02 v0.20.0
### バグ修正
- トップの入力フォームを使用しない設定にすると管理者ログインの時にもトップのフォーム、そして画像アップロードのフォームが表示されなくなるバグを修正しました。  
管理者のみアップロード可にしたいときに、アップロードができなくなっていました。  
管理者投稿モード(日記モード)でログインしているときは、トップの入力フォームと画像アップロードのフォームが表示され、コメントのみの投稿も画像アップロードもできるようになりました。
### 改善
- 動画を表示する画面からの戻り先のリンクを掲示板のトップページから、個別スレッドに変更しました。
動画再生画面から掲示板の該当スレッドに戻れるようになりました。

安定版をリリースからダウンロードできます。  
[Petit Note v0.21.6 リリース](https://github.com/satopian/Petit_Note/releases/latest)

##  22/06/19 v0.21.6
### バグ修正
- 名前クリック時の作者検索が正しく動作しなくなっていたのを修正しました。  
v0.18.10、lot.220522で発生したバグです。
### 改善
- ChickenPaintが全画面表示で起動するようになりました。
- メインページとカタログページのページ番号が番号の途中で改行されないようにしました。
- 現在ページの番号を太字で表示するようになりました。
- 管理者ログイン時の確認処理に使用している第2パスワードの存在チェックを処理に追加しました。
- 指定経過日数を超えた古い投稿でも管理者は続きを描けるようになりました。  
指定経過日数を超えた古い投稿はユーザーによる編集、続きを描くができなくなるようにしてあります。  
管理者は編集が可能でしたが、続きを描くはできなくなっていました。  
管理者は編集、削除、続きを描く、画像差し換えすべての機能を制限なく使えるようになりました。  

##  22/05/31 v0.19.6

- レス先のスレッドの番号が1000を超えている時にレスでお絵かきできなくなるバグを修正しました。
レス先の番号が1000以上の時にレスでお絵かきすると｢問題が発生しました｣というエラーメッセージが表示されて投稿できなくなるバグを修正ました。


##  22/05/29 v0.19.5
- v0.18で発生した指定サイズ以上の実体データの縮小処理が効かなくなるバグを修正しました。
- 画像差し換え時の指定サイズ以上の実体データの縮小処理が抜けていたを修正しました。

##  22/05/28 v0.19.2
### 画像差し換え機能を追加

![220528_petitnote](https://user-images.githubusercontent.com/44894014/170832344-52d5efbb-802b-48f1-9ac5-4ee106b6232e.gif)

アップロードした画像を差し換える事ができるようになりました。
修正した画像と差し換えたい時などにご利用いただけます。

### スクロールすると出てくる上に戻るボタンを追加

![image](https://user-images.githubusercontent.com/44894014/170833452-db5c4ce0-b595-49ff-9abb-f06372391bce.png)

多くのウェブサイトに実装されている上に戻るボタンを実装しました。

### ログファイルが壊れないようにするための多くの変更

- スレッドの親が1行目にある事を厳密に確認してから、スレッドのレスを作成するようになりました。   
ファイルロックがかかった状態で、1行目が親である事を確認してから処理を行うようになりました。  
一瞬の隙をついたタイミングで問題が発生する可能性がゼロではないため対策を行いました。
 
### 拒絶するURLが設定可能になりました

config.phpに新規設定項目を追加しました。
その設定が特に必要ない方は従来のconfig.phpをそのままご利用ください。

### バグ修正
- スパムの拒絶処理で、拒絶する文字列の指定に`/`(スラッシュ)が含まれる時に処理が失敗するバグを修正しました。
- お絵かき画像投稿時のコメント欄でURLを入力しても反映されないバグを修正しました。
- アップロード画像の作業ファイルのゴミが残るバグを修正しました。


##  22/05/04 v0.15.3
## 重大なバグを修正
- ｢続きを描く｣ができなくなる大きなバグがv0.12で発生していました。
v0.12は使用しないようにしてください。
index.phpの上書きアップデートをお願いします。

##  22/04/28 v0.12.1
### Klecks更新
- iPadOSで発生するいくつかの問題が修正されました。
- 使用可能な言語に繁体字中文が追加されました。

### 改善
- 必要なファイルの存在をチェックする機能を追加しました。
設置や移転の時のための機能です。
必要なファイルが存在しない時は、エラメッセージでファイルの場所とファイル名を表示します。

- klecksの送信失敗の原因がサーバーエラーの時はエラー番号をアラートで表示します。
例えば、Klecksのデータを受信する`saveklecks.php`が存在しない時は、｢エラー404｣というアラートを表示します。

- ファイルサイズが指定サイズよりも大きなときに、PNGからJPEGに変換する処理の作業ディレクトリを`temp/`に変更しました。
これにより、処理に失敗して作業ファイルのゴミが残っても、テンポラリの掃除機能で不要なファイルとして自動的に削除されるようになります。

### バグ修正
- 全体ログのパスワードが一致しなかった時に処理が停止せず、スレッドのログファイルの画像やログが先に削除されてしまう箇所がありました。
編集、削除、続きを描くの画像差換えの3箇所です。
全体ログのパスワードが一致しない時は、スレッド個別のログファイルにかかわる処理が実行されないように書き直しました。

- config.phpの設定で、
`$deny_all_posts = true;`//全ての投稿を拒否
に設定した時に、返信ボタンに｢返信｣と表示されていたのを｢表示｣に修正しました。
古いスレッドを閉じた時、1スレッドあたりの最大投稿数を超過した時と同じ動作になるように調整しました。


##  22/03/17 v0.11.8 
### 改善
#### Klecksの日本語訳
![image](https://user-images.githubusercontent.com/44894014/160145766-395c519f-e90e-4397-a92e-03005648906e.png)

- Klecksが多国語対応したのに伴い、日本語翻訳版を作成しました。  
PetitNoteにも、日本語対応版を同梱する事ができました。
この新しいバージョンのKlecksは、ブラウザの言語の優先順位を自動検出して言語を切り替えてくれます。  
また、ブラウザの言語の設定にかかわらず使用する言語を指定する事もできます。  
英語、ドイツ語、日本語が選択できます。  
中文は簡体字のみで細部はまだ英語のままです。  
日本語翻訳版はすでに開発元に統合済みです。

####  透過PNG、透過GIFのサムネイルの透明部分を白に変更  

- 透過PNGの透明部分がJPEG化する時に、真っ黒になっていたのを修正しました。  
透明色が黒も間違いではないのですが、意図しない結果になる事が多いため、透過GIF、透過PNGからJPEGに変換する時は、透明色を白に変換します。  

#### ファイルサイズチェックの方法を変更  

- ファイルサイズの上限のチェックが、アップロード前のファイルサイズだったのを修正しました。  
アップロード処理でファイルサイズが減少した後にファイルサイズをチェックする方式になりました。  

### バグ修正

- 管理者ログイン時に使うアップロードペイントアプリ固有形式、pch、chi、psdなどの不要になったファイルの自動削除機能の動作時に軽微なエラーが発生するケースがあったのを修正しました。


##  22/03/17 v0.10.8 
### 改善
### アプリ固有ファイルのダウンロードボタンができました。
![image](https://user-images.githubusercontent.com/44894014/158780127-5f6fb530-0043-4132-8ea4-f662b2a710fd.png)

#### アプリ固有形式一覧
- `.pch`ファイル(PaintBBS)
- `.chi`ファイル(ChickenPaint)
- `.psd`ファイル(Klecks)

Klecksのレイヤー情報を含むファイルはPhotoshop形式の`.psd`ファイルです。 
ダウンロードした`.psd`ファイルはクリスタやSAIそのほか多くのアプリで開く事ができます。  
`.pch`と、`.chi`は、それぞれNEOとChickenPaintで開く事ができます。    
管理者投稿モードでログイン時に`.pch`、`.chi`、`.psd`を添付してペイントボタンを押せば、キャンバスに読み込んで投稿できます。  

##  22/03/14 v0.10.5.1 
### バグ修正
- iPad+Apple Pencilでアプリのメニューが操作できなくなっていたのを修正しました。  
ペイント画面から問題の発生の原因になっていたJavascriptを削除しました。  
### Klecks更新
- 新しいブラシが追加されました。左右対称、上下対称のミラーペインティングができるようになりました。  


##  22/03/10 v0.10.5

![image](https://user-images.githubusercontent.com/44894014/157668975-fff6786b-c9dd-43cf-9dba-732829f47912.png)

新しいリリースの確認を簡単にするため、管理者メニューに最新のリリースのバージョンを表示します。
このバージョンの画像をクリックすると、GitHubの最新のリリースのページが開きます。

config.phpに新規設定項目を追加しました。

##  22/03/09 v0.10.3
### 新しいペイントアプリ｢Klecks｣が使えるようになりました。
![image](https://user-images.githubusercontent.com/44894014/157258620-01f053e9-1bd1-47d0-a573-5c8aae432cce.png)

わかりやすいUIと強力なブラシが使えるアプリです。
レイヤーの最大数は16枚です。
数多くのフィルタが使えます。輝度を透明に変換、明るさ/コントラスト、色調補正など。

このアプリの追加にともない、管理者投稿モードのときにアップロードできるファイル形式に｢PSD｣が追加されました。  
PSDファイルを選択してペイントボタンを押すと｢Klecks｣のキャンバスにPSD画像が読み込まれます。  
トップページからのpch、chi、psdのアップロードペイントだけでなく、返信画面からのpch、chi、psdの投稿もできるようになりました。  

### バグ修正
- スレッドのレス表示件数がページの下になるにつれ1ずつ増えるバグを修正しました。
- 未定義エラーを修正しました。


##  22/02/12 v0.9.18.0
## 個別スレッドのファイルの編集時にファイルロックがかかっていませんでした。
このバグによりログが破損する可能性があります。
通常は編集、または書き込みが同時に行われても一瞬でも先にファイルを開いた側が他からファイルを読み込めないようにロックします。 
そのロック処理が二箇所抜けていました。
その他の機能追加が特に必要ではない方も、以下の2つのファイルの上書きアップデートをお願いします。    

### 変更があったファイル
- functions.php 
- index.php   


## 22/01/06 v0.9.12.5

- 編集削除時のパスワードチェック処理を変更しました。レスのログファイルのパスに加えて全体ログのパスワードをチェックするようになりました。

- レス画像から続きを描く時は、新規投稿でもレスになりました。

- レス画面に前のスレッドと次のスレッドが表示されるようになりました。

![image](https://user-images.githubusercontent.com/44894014/151515726-56ed8a8f-0073-4871-baa3-f1338d6f2f94.png)


- 続きから描くからの｢もどる｣のリンク先を該当スレッドに。  
これまでは掲示板のトップページにもどっていました。そのため｢続きを描く｣の画面がGoogle検索でヒットしても、もとのスレッドがどこにあるのかわかりませんでした。  
 
- 画像チェックの負荷を削減しました。

- テンプレートのエスケープ漏れがあってもXSSが実行されないように編集画面の変数をHTMLファイルに渡す前にエスケープしました。  

- iPadの768pxで閲覧時に画像の右側の余白がでないように調整しました。  
768px以上の幅の画像を表示する時は右側のmarginを0にフロートをnoneに。

- 入力文字列、拒絶する文字列どちらからもスペースを除去。拒絶する文字列にスペースがはいっていても機能するようになりました。  
これまでは拒絶する文字列の設定に半角スペース、全角スペースがあると、入力文字列にスペースがあっても拒絶できなくなっていました。  
これは、入力された文字列からスペースや改行をとりのぞいた文字列をチェックしているからです。  
拒絶する文字列に入っているスペースもチェック時に除去する事でこの問題を解決しました。

- 文字化け対策。投稿者名をコピーで使用する時は特殊文字を全角に。  
セキュリティを確保しながらかつ文字化けが最低限になるようにするためHTMLの特殊文字を全角に変換します。 
投稿者名をコピーの箇所のみの対応でそのほかの箇所はもとの入力文字列が表示されます。

- コメントの最小幅を350pxに。
より見やすい画面になりました。

## 2021/12/05 v0.9.9.2
- 英語対応。ブラウザの言語が日本語以外の時は、UIとエラーメッセージを英語で表示します。

### 変更があったファイル
- functions.php 
- index.php 
- picpost.php 

 template/basic/ ディレクトリのすべてのファイル(含むCSS)


### 追加されたファイル
- palette_en.txt 
(英語表示の時のためのパレット)


## 2021/11/27 v0.9.8.28

- sageにチェックが入っていなくても、レスでスレッドがあがらないようにする設定項目を追加しました。
```
//する: trueに設定するとレスがついてもスレッドがあがりません。(全てsage)。
//初期値 false

//$sage_all = true;
$sage_all = false;

```
- HTMLの文法エラーを修正しました。


## 2021/11/23 v0.9.8.26
- chiファイルアップロードペイントファイルの削除処理  
管理者投稿でChickenPaint固有ファイル、chi形式のファイルをアップロードしてキャンバスに読み込んだあとのchiファイルの削除処理が抜けていたのを修正、追加しました。  
今回の修正でアップロードから5分経過していればtempディレクトリから削除されるようになりました。この修正を行う前でも、数日経過すれば不要になったファイルは削除されていました。

- 編集削除のIDとして使っている投稿時間が重複しないように入力値を検証してエラーにする  
同じ記事ナンバーかつ同じタイムスタンプとなる可能性を完全に排除しました。  

- 画像のALT文の見直し。続きを描く時の画像にもイラストのタイトルと作者名  
画像のALT文にタイトルと作者名が入るようになりました。  

- HTMLの文法ミスを修正しました  


## 21/11/13 v0.9.8.18.2
### PaintBBS NEO v1.5.15 の右ボタン常時表示に対応
- PaintBBS NEO v1.5.15 の右ボタン常時表示に対応しました。
`neo.js`と、`paint_neo.html`のアップデートをお願いします。  
また、ブラウザの言語が日本語以外の時に表示されるPaintBBS NEOの英語表記版の半角文字列の改行が意図通りに行われずレイアウトがくずれていたのを修正しました。  
`paint_neo.html`のアップデートをお願いします。

v0.9.8.18.1に更新したファイルが入っていなかったため、改めて更新をお願いします。  


## 21/11/13 v0.9.8.18.1
### picpost.php save.php
- 簡易的なCSRF対策を行いました。  
`picpost.php` `save.php` と、`index.php`のアップデートをお願いします。

- ~~PaintBBS NEO v1.5.15 の右ボタン常時表示に対応しました。~~
~~`neo.js`と、`paint_neo.html`のアップデートをお願いします。~~  
~~また、ブラウザの言語が日本語以外の時に表示されるPaintBBS NEOの英語表記版の半角文字列の改行が意図通りに行われずレイアウトがくずれていたのを修正しました。~~  
~~`paint_neo.html`のアップデートをお願いします。~~


## 21/11/08 v0.9.8.16
### index.php
- Descriptionが長くなりすぎる問題に対応しました。  
これまではスレッドの親のコメント全文がDescriptionに入っていました。

## 21/11/03 v0.9.8.12

- config.phpに新規設定項目追加  
- コメント欄に投稿可能な最大文字数を設定できるようになりました。 
- 投稿できる画像の幅と高さを設定できるようになりました。サイズ超過の時は設定したサイズの範囲内になるように自動的に縮小します。  
index.phpとthumbnail_gd.phpを同時に更新する必要があります。
thumbnail_gd.phpのバージョンが古い時は、バージョンが古いというエラーメッセージがでます。通常通り起動していれば更新に成功しています。

- save.phpを更新しました。ChickenPaintによる投稿の時に画像の幅と高さのサイズ違反をチェックするようになりました。
- picpost.phpを更新しました。PaintBBSNEOによる投稿の時に幅と高さのサイズ違反をチェックするようになりました。
- template/basic/ ディレクトリの index.css を更新しました。長い英数字の時に文字列がコンテナを突き抜けて横に長く表示されてしまう問題を解決しました。

## 21/10/29 v0.9.8.9
- 重大バグ修正 urlの長さチェックを追加しました  
- エラーメッセージurlが長すぎますを追加しました。  

## 21/10/29 v0.9.8.7.2  
ログファイルを外部から直接開かれる事が無いよいうにパーミッションを600にしているログファイルですが、さらに`.htaccess`というファイルを追加して、拡張子がlogのファイルを外部から開けないようにしました。
`.htaccess`を`index.php`と同じディレクトリにアップロードします。

## 21/10/27 v0.9.8.7.1
- 著作リンクを変更しました。templateのリンク先が変わっただけです。  
新url [https://paintbbs.sakura.ne.jp/](https://paintbbs.sakura.ne.jp/petit/)


## 21/10/22 v0.9.8.7
- csv(tsv)としてログファイルを読み込んでいたため、ダブルクォートが入力された時にデータが壊れていました。  
重大なバグですので、アップデートが必要です。

## 21/10/13 v0.9.8.3
- お絵かきアプリの幅と高さのcookieが正しく処理されていなかったのを修正しました。
高さのcookieが反映されていませんでした。
- 画像のファイルサイズが1MBを超えている時は幅と高さが範囲内でもサムネイルを表示する形に変更。
GIFアニメのアップロードを行っても表示が重くならないように。

- 削除時に記事がチェックされていない時はエラー表示にする。
これまでは、記事削除の最終確認のチェックを入れ忘れていた時に何も起こりませんでした。

- 読み込みだけの処理なのにfopenの"r+"で開いている箇所があったのを"r"に修正しました。

- 指定日数を超える古い記事の編集禁止。
古いスレッドを閉じる処理はありましたが、編集はできていました。
古い記事の編集はロックされますが、削除はできます。
また管理者は古い記事の編集と削除どちらもできます。

## 21/10/13 v0.9.7.3 
- 新しいスレッドを行末に追加する仕様を変更し行頭に。従来の`alllog.log`を逆順に。  
[v0.9.7で仕様変更、v0.9.6.3以前のalllog.log(全体ログ)の変換が必要になりました。 · Issue #6 · satopian/Petit_Note](https://github.com/satopian/Petit_Note/issues/6)  
ログファイルの変換が必要になりました。  
上記リンク先にログファイルの変換方法の詳細をまとめました。お手数をおかけしますがよろしくお願いいたします。  


## 21/10/11 v0.9.6.3

- 管理者編集モードで編集に失敗するバグを修正。
- 最下部の｢管理｣メニューが2重に表示されるバグを修正。
- 管理パス、第2パス未設定時にはパス不一致とする処理を追加。


## 21/10/11 v0.9.6.1

- 名前の入力を必須にする、しないを設定できるようにしました。
- sage機能を追加しました。
- config.phpに新規設定項目。第2パスワードを使って管理者である事を再確認する処理を追加。 

## 21/10/09 v0.9.3.3

- セキュリティ対策。
- ログイン時にsessionIDを再発行してsession固定攻撃対策。
- 編集･削除時にcsrfによる処理が行われないようにトークンをセット。  
これまでは、削除の時にはトークンがセットされていませんでした。
- sessionのクッキーの範囲を掲示板のカレントディレクトリに限定。  
これまでは複数設置したPetit Noteのモードが同時に変更されていました。  
操作する人は同じ人とはいえ、他のディレクトリのアプリに影響がでるのはよくない事なので、アプリのカレントディレクトリ別のsession IDとクッキーを使用する形に変更しました。

## 21/10/06 v0.8.1

- 日記モードで使用していても画像でレスができる状態だったため、レスで画像アップロードを使う･使わないを設定できるようにしました。

## 21/09/23 v0.7.5

- 編集時にタイトル欄を空にした時にも｢無題｣と入るようにした。レスの題名をスレッドの親のタイトルにRe:を付けたものに。
- レスの時は親のタイトルを自動で入れる。ただし掲示板には表示されない。外部プログラム使用時に必要。
- お絵かきコメントのJavaScriptの修正。
レスでお絵かきの時に題名欄が表示されないようにする工夫ですが、動作していれば従来通りでも問題ありません。 

## 21/09/23 v0.6

- 記事の編集･削除。続きを描く、管理者認証マークの表示。カタログ機能。投稿者名の名前で記事の一覧。メール通知機能。  
ログファイルの拡張に区切をつけて、ログファイルの形式をいったん確定。

## 21/09/06 v0.02
- 投稿時のパスワードをパスワードハッシュで保存。
- ユーザー削除機能を追加しました。
- 日記モードができました。
- 日記モードの時は、スレ立てができるのは管理者のみになり、フォームを偽装して投稿してもエラーになります。
- 管理者削除と日記モードログインのための管理者ログインページができました。

## 21/09/03 v0.01
- ~~続きを描く機能はありませんが、~~ NEOとChickenPaintで絵を描いて投稿する事ができます。
- 管理者モードにログインすると記事の削除が可能になります。
- ~~ユーザーのパスワード入力欄はまだないので、ユーザーによる編集や削除もできません。~~
- 合言葉機能を使えば、合言葉を知っている人しか投稿できなくなります。入力フォームもでません。
- 1スレッドに投稿できるレスの数を超えると入力フォームが消えます。さらにフォームを偽装して投稿してもエラーになります。
- レスがついたスレッドが一番上に表示される仕様。
- 古いスレッド判定も投稿順ではなく、最新レス順です。
- レスポンシブデザイン。スマホ･タブレットに対応しています。
- HTMLファイルを外部化して、1枚のHTMLファイルとして扱う事ができるため、ユーザーによるデザインの変更が容易です。
