---
layout: post
title: Jekyllカスタマイズへの道 その3
data: 2020-02-12
categorues: blog
tags: jekyll html css
---
## レスポンシブデザイン

最近のサイトはパソコンで見た時とスマフォで見た時の見た目が微妙に違うサイトが多い．
これは異なるhmtlファイルを作っているのではなく，同じコンテツ(内容)の配置を画面のサイズで変えているらしい．

なのでこのブログにも実装してみる．

## 画面のサイズに合わせて表示領域を変える

CSSでは`@media`という@-規則を使用するらしいので
今回はサンプルとしてindex.htmlとstyle.cssを作って一度試してみた.

```html
index.html

<!doctype html>
<html>
    <head>
        <meta charset="utf-8">
        <link rel="stylesheet" type="text/css" href="style.css">
    </head>
    <body>
        <p>test</p>
    </body>
</html>
```

```css
style.css

@media screen and (min-width: 300px){
    body{
        color: red;
    }
}

@media screen and (min-width: 600px){
    body{
        color: blue;
    }
}


@media screen and (min-width: 800px){
    body{
        color: yellow;
    }
}
```

これでブラウザの横幅を変えると一番狭くして赤，少し大きくして青，最後に黄色に文字の色が変化する.

@mediaの後ろにあるscreenはメディアタイプを示していて

- all
- print
- screen
- speech

の種類がある．
今回は主に画面のためのものであるscreenを選択して,andで画面サイズの条件を付け加えている．

## 実際に適用してみる

サイトをレスポンシブにするためには`<head>`に新しく`<meta>`を追加する必要があるのでまずはそこから始める．

\_layout/default.htmlに

```html
<meta name="viewport" content="width=device-width,initial-scale=1,maximun-scale=1.0, user-scalable=no">
```

を追加する．

viewportは初期の画面のサイズに関する設定で
**モバイル端末** のみに適応される．

width=device-widthで端末の画面のサイズを初期値として使用し，

initial-scaleで画面とデバイスの幅の比率を設定している．

user-scalableはページのズームをユーザにさせなくする設定だが
最近のブラウザだと意味がないらしいのでなんとなくnoにしてみた．

あとは実際のcssの設定を書き換えて完了．
assets/css/style.cssの対象を

```css
@media screen and (min-width: 768px) {
	main {
		width: 50%;
		margin: 0 auto;
	}
}

@media screen and (max-width: 768px) {
	main {
		width: 50%;
		margin: 0 auto;
	}
}

@media screen and (max-width: 375px) {
	main {
		width: 80%;
		margin: 0 auto;
	}
}
```

今回はこのようにした．

[参考資料]<br>
[\<meta\>: 文書レベルメタデータ要素 - HTML: HyperText Markup Language \| MDN](https://developer.mozilla.org/ja/docs/Web/HTML/Element/meta)<br>
[メディアクエリ - CSS: カスケーディングスタイルシート \| MDN](https://developer.mozilla.org/ja/docs/Web/CSS/Media_queries)
