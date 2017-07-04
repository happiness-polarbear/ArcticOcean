# HPNS-001_GitPitchを利用して複数人でスライド管理＆知見を蓄える
<span style="font-size:0.6em; color:gray">date: 2017/07/07 | author: ama</span>

---
## 目次
- はじめに
- GitPitchとは
- 使用方法
- 設定オプション
- コードプレゼンテーション機能
- 複数人での運用
- フォルダ構成
- 作業手順
- 感想・問題点

---
## はじめに

---
## GitPitchとは

- Gitリポジトリ内の、PITCHME.mdを、オンライン及びオフラインでスライドに変えるサービス  |
- GitHub、Bitbucket、Gitea、Gogs、GitLabの、Gitリポジトリサービスと通信ができ利用可能 |
- デフォルトでは、GitHubと通信するように設定されている |
- CSS3/JavaScriptで作られたプレゼンテーションソフトウェアのreveal.jsをスライド表示に使用 |
- https://gitpitch.com/ |

+++

### GitHub以外のサービスを利用するには

- GRS（Git Repository Services）クエリパラメータを手動で指定する

```
`https://gitpitch.com/user/repo/branch?grs=service`
```

- スライド左下隅にある切り替えメニューで切り替える

---
## 使用方法

- リポジトリ作成 |
- PITCHME.md マークダウンファイルを作成 |
- PITCHME.mdを編集してコミット&プッシュ |
- `https://gitpitch.com/[GitHubのユーザー名]/[リポジトリ名]` |

---
## 設定オプション

PITCHME.yamlファイルを使用して、オプション設定が出来る。

+++
### テーマ設定
```
theme : moon
```

- テーマの種類は、black, moon, night, beige, sky, whiteから選択できる。

<br />
### アイコン設定
```
logo : hpnsAma/images/logo.jpg
```

- スライドの左上隅にアイコンが設置できる。

+++

### 背景設定
```
background : hpnsAma/images/bg.jpg
```

- オリジナルの画像をスライド背景に設定ができる。

<br />
### 背景サイズ設定
```
background-size : cover
```

- デフォルトだと、背景画像はスライドの幅100%、高さ100%になるように引き伸ばしされている。
- background-size: auto, contain, cover の設定できる。

+++

### ハイライト設定
```
highlight : monokai
```

- コードブロックの構文ハイライトのカスタマイズができる。
- [カスタマイズデモ](https://highlightjs.org/static/demo/)

<br />
### スライド番号設定
```
slide-number: true
```

- スライド右下隅にあるスライド番号カウンターを有効・無効に設定できる。

+++

### 著作権表記の設定
```
footnote : "© 2017 y-ama"
```

- スライド左下隅に著作権表記が設定できる。

+++

### 数式表記の設定
```
mathjax : TeX-MML-AM_HTMLorMML-full
```

- 数式表記設定をすると、MathJaxを有効にしてカスタマイズすることができる。
- MathJax→テキストベースのコマンドをWeb上で数式に整形・表示するオープンソースのJavaScriptライブラリ
- [MathJax公式ページ](https://www.mathjax.org/)

+++

### 垂直センター設定
```
vertical-center : false
```

- デフォルトでは、垂直配置設定が有効になっている→コンテンツはスライド中央配置になっている。
- スライドの垂直センター設定を無効にするときに設定する。

+++
### カスタムCSS
```
theme-override : assets/css/PITCHME.css
```
- 選択したテーマのスタイルシートを上書きするカスタムCSSを作成
- Gitリポジトリに追加
- PITCHME.yamlに登録

+++

### オートスライド設定
```
autoslide : 5000
```

- 自動スライド設定が可能（↑の例だと5秒間隔でスライド）
- 個々のスライドスピードを変更したい場合は、PITCHME.md内のスライドの先頭に下記を記述

```
<!-- .slide: data-autoslide="10000" -->
```
- スライド先頭記述で、10秒表示される。記載が無い場合は5秒間隔でスライドされる。

+++

### ループ設定
```
loop : true
```

- 最後のスライドから、最初のスライドへナビゲーションを許可することができる。
- 注） オートスライド設定も有効になっていると、停止しない限り、ずっとループされる。

+++

### RTL設定
```
rtl : true
```

- 右から左へのナビゲーションスライドを設定できる。
- デフォルトは、左から右へのスライド。

+++

### 移行設定
```
transition : fade
```

- スライドのエフェクトを指定することができる。
- エフェクト種類： convex, concave, default, fade, none, slide, zoom
- デフォルトでは、slideエフェクト使用

### マウスホイール設定
```
mousewheel : true
```

- マウスホイールを使用したスライドナビゲーションを許可することができる。

+++
### 現状の設定
```
#テーマ設定
theme : white

#アイコン設定
logo : hpnsAma/images/logo.png

#カスタムCSS設定
theme-override : /CSS/PITCHME.css

#スライド番号設定
slide-number: true

#著作権表記の設定
footnote : "© 2017 y-ama"
```

---
## コードプレゼンテーション機能

+++
### コードを埋め込むには
<br />

- マークダウンのコードブロックを使用 |
- GitPitch コードデリミタスライドを使用 |
- GitPitch GISTスライドを使用 |
- GitPitch イメージスライドを使用 |

+++
### GitPitch コードデリミタスライドを使用
<br />
Gitリポジトリ内の任意のファイルから、プレゼンテーション内の任意のスライドのコードブロックに、コードを読み込むことができる。

```
---?code=path/to/source.file
```

+++
### GitPitch GISTスライドを使用
<br />
スライドにGitHub GISTを埋め込むには、PITCHME.mdファイルにGIST識別子を指定する。

```
---?gist=cf4227416b55dac54a53
```

---
## 複数人での運用

+++

## フォルダ構成

```
ArcticOcean（repo）
 |
 |- CSS
 |   |- PITCHME.css
 |
 |- hpnsXXX
 |   |- FIX
 |   |- images
 |   |- PITCHME.md
 |   |- PITCHME.yaml
 |
 |- hpnsXXX
 |   |- FIX
 |   |- images
 |   |- PITCHME.md
 |   |- PITCHME.yaml
 |
 |- hpnsAma
 |   |- FIX
 |   |   |- HPNS-001_PITCHME.md
 |   |   |- HPNS-002_PITCHME.md
 |   |
 |   |- images
 |   |   |- HPNS-001
 |   |   |      |- hoge.png
 |   |   |
 |   |   |- HPNS-002
 |   |   |      |- hoge.png
 |   |
 |   |- PITCHME.md
 |   |- PITCHME.yaml
 |
 |- README.md
```

+++
### ブランチ運用

```
master
↓   ↑
↓   ↑ PR
↓   ↑
hpnsXXX
```

+++

### スライドアクセス方法

`https://gitpitch.com/user/repo/branch?p=hpnsAma`

- "?p=hpnsAma"で管理フォルダを指定してあげて、ユーザー（スライド）切り替え

---
## 作業手順
- リポジトリを任意の場所にクローン
- 作業フォルダに行き、config設定（※変更不要なら不要）

```
cd HPNS-PBR
git config user.name "y-ama"
git config user.email "happiness.polarbear@gmail.com"
```

- masterブランチから、作業ブランチhpnsXXXを作成
- 作業フォルダを作成し、PITCHME.md、PITCHME.yaml、imagesフォルダ、任意フォルダを作成

+++

- PITCHME.mdにスライド内容をマークダウンで記述
- PITCHME.yamlに、オプション設定を記述
- 初期コミットを行ったら、masterブランチとのPRを作成
- 作成完了したら、メンバー内でレビューを行い、指摘をもらう
- メンバーの指摘を反映したら、発表できる段階になり、masterへマージする
- プレゼンテーション

+++

- 発表後、HPGメンバー指摘内容でスライドに反映するものがあれば更新
- 更新が終わったら、マークダウンファイルをコピーしてFIXフォルダに入れ、スライド内容が分かる内容のタイトルで追加
- masterにマージして終了

---
## 感想・問題点
- プレビュー機能が無いので、どの程度のテキスト量を入れればバランス良いか分からなかった
- PITCHME.cssを利用して、オリジナルのスライドを模索する必要がある

---
## 終わり