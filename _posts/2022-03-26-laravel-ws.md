---
layout: post
title: dockerでlaravelの開発環境構築
data: 2022-3-26
categorues: tech
tags: laravel
---

## 構築環境

amazon linux 2のイメージを元にlaravel,nginxが動作するコンテナを作成する.
また、データベースにはpostgresを用いる.


## コンテナ作成

[laravel-ws](https://github.com/link-forte/laravel-ws)をcloneして
srcという名前でlaravelのプロジェクトを設置する
(設定ファイルを直接触ればディレクトリ名はなんでも可).

以下のコマンドでコンテナを作成し、
localhost:8080でアクセスできることを確認する.

```bash
$ docker compose up -d --build
```


## laravelのプロジェクトを1から作る

コンテナ作成後に以下のコマンドでappコンテナに入り
composerを使用しlaravelの環境を構築することも可能である.

```bash
$ docker compose exec app bash
```

以下はappコンテナ内で実行.

```bash
$ composer create-project laravel/laravel src
```
