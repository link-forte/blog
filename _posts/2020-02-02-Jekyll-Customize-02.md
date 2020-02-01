---
layout: post
title: Jekyllカスタマイズへの道 その2
date: 2020-02-02
categorues: blog
tags: jekyll html css
---
## 流行りに乗って左右を開けて中央揃えに．
Postのカスタマイズを実践して行く．

最近のブログはコンテンツは中央にあって,
左右が空いてるイメージがあるのでまずは
それから真似てみる．

## ファイル構成

初めに最終的なhtmlファイルが出来るまでにどのような流れで
レイアウトが構成され行くのかを確認する．

layoutはdefault.htmlとpost.htmlに分かれている．
呼び出される順番としては

1. default.html
2. post.html
3. ブログpostの.md

の順番になっている．

これは，ブログpost.mdでlayoutとしてpost.htmlを読み込んで,
読み込んだpost.htmlでdefault.htmlを読んでいるため．

default.htmlには`<head>`があり`<meta>`タグなどの
実際にページに表示はされないが大事な事が書かれている.

`<body>`で囲まれた\{\{ content \}\}にpost.htmlの中身が展開される.

post.htmlには実際に画面に表示される部分が書いてある.
`<header>`や`<main>`,`<footer>`などの分けて情報を表示している．

`<header>`にはタイトルと日付を，`<footer>`にはコピーライトを置いている．

`<main>` で囲まれた\{\{ content \}\}にブログpost.mdが展開されて記事なる．　

## コンテンツを中央に

本題の記事を中央に配置する．

上で書いた通り，画面に表示される部分は`<body>`タグで囲まれているので
これを中心にCSSでカスタマイズして中央に配置されるようにする．

一番外側の横幅を決めるため,
assets/css/style.cssに

```css
body{
    width: 100%
}
```

を追加する．
widthは要素の横幅を決める設定で
これで横幅をブラウザの画面横一杯まで使えるよになった．

次に実際に記事が表示される`<main>`に

```css
main{
    width: 50%;
}
```

を追加する．
これで`<main>`の横幅が`<body>`の50%になる．

しかし，このままだとまだ全体が左に寄っている．
なので追加でmarginを追加する．

```css
main{
    witdh: 50%;
    margin: 0 auto;
}
```

これで左右に均等に余白が取られて記事が中央に表示されるようになった．

次回は装飾をしたい．

今回出てきたが説明していないmarginを含めて要素の

- margin
- border
- padding

を設定していきたい．

[参考資料]<br>
[HTML: HyperText Markup Language \| MDN](https://developer.mozilla.org/ja/docs/Web/HTML)<br>
[CSS: カスケーディングスタイルシート \| MDN](https://developer.mozilla.org/ja/docs/Web/CSS)
