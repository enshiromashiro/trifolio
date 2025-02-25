# trifolio 設計メモ

自分のウェブサイト用に軽い静的サイトジェネレータがほしい。

## コンセプト

### つくりたいウェブサイト

- 個人サイト
    - 絵の一覧、ブログメモの記事集、ふつうのページ

### あってほしい機能など

- GFMとAsciiDocによる静的サイトジェネレータ
- コンテンツの格納構造とサイト構造の分離
    - あと状態 (追加した日とか更新した日) も分離したい
- ブログのようなコンテンツ集合の一覧を別ページに埋め込める
    - 埋め込み式indexページ
- 「ウェブサイトプロジェクト」は次のもので構成される:
    - コンテンツ: 内容部分の情報 (.md、.adoc、メディアファイル)
    - リソース: レイアウトや見た目の情報 (メディアファイル、テンプレート、.jsや.css)
    - サイト構造: コンテンツやリソースがどのようなパスに落かれるかの情報
- 「コンテンツバンドル」
    - 1つのコンテンツを複数のコンテンツで表現するもの
    - ブログ記事、絵一覧
- mathjaxやmermaidの導入 (必要なページのみ)
- 出力数とコンテンツ構成ファイル数の不一致に注意
    - 出力が単体でも複数ファイルから構成されるものがありうる
    - 長文の記事 (章立てをファイル分割とか)

### メモ

- テンプレート機能
    - Jinjaっぽいのでいいかーとおもっている
    - これ: https://keats.github.io/tera/docs/

## 設計

### コンテンツについて具体的なところ

- コンテンツの参照の仕方: `[../親コンテンツのファイル名/]コンテンツのファイル名`
    - ところでリンクを実際の構造に即したパスに書き換えねばでは…？
    - リンク先やimg要素のsrc属性とかでコンテンツID書いてあるときに…
    - これが問題になるのはマークアップコンテンツのみ
        - 各形式で正しく書き換えできれば問題はない
        - パーサが構文木とれればいいが…
- コンテンツの種類それぞれに拡張子やディレクトリ構造が定まってる感じ
    - 単体ページ (.md or .adoc or HTMLパーツ)
    - 単体画像
    - 記事集
    - 絵一覧 (絵と説明)
    - OGP
- ↑ これはリソースも?

### ディレクトリ構造

```
contents/
  top.md                         ... single-file content, ID: `top`, type: page
  about.adoc                     ... single-file content, ID: `about`, type: page
  # WIP: page bundle structure
  articles/                      ... multiple-file content, ID: `articles`, type: page bundle
    _page_list.md                ... list page template?
  # WIP: resource bundle structure
  drawings/
    _resource_list.md            ... list page template?
# NOTE: templates are contents? (like "list page template?")
templates/
resources/
.state/
site_config.toml                 ... config file for: website strucuture, output settings, ...
```