MiddleMan入門
======================

# 目的 #
MiddleManを使ってサイトの作成・更新が出来るようになる。

# 前提 #
| ソフトウェア   | バージョン   | 備考        |
|:---------------|:-------------|:------------|
| OS X           |10.8.5        |             |
| ruby           |1.9.3p392     |             |
| middleman      |3.2.0         |             |


# 構成 #
+ インストール


# 詳細 #

## インストール ##

    $ rvm gemset create middle_man
    $ rvm use ruby-1.9.3-p392@middle_man
    $ gem install middleman

## 新しいサイトの開発を始める ##

    $ middleman init introduction
    $ tree introduction/
    introduction/
    ├── Gemfile
    ├── Gemfile.lock
    ├── config.rb
    └── source
        ├── images
        │   ├── background.png
        │   └── middleman.png
        ├── index.html.erb
        ├── javascripts
        │   └── all.js
        ├── layouts
        │   └── layout.erb
        └── stylesheets
            ├── all.css
            └── normalize.css

## 開発サイクル ##

1. サーバー起動

        $ cd introduction
        $ middleman server

1. ブラウザで確認

        http://localhost:4567/

1. 静的サイトのエクスポート

        $ cd introduction
        $ middleman build

## プロジェクトテンプレート ##

# 参照 #
[MiddleMan](http://middlemanapp.com/)

[MiddleMan日本語ページ](http://middlemanjp.github.io/)
