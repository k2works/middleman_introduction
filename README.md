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
+ はじめに
+ テンプレート
+ Frontmatter
+ 動的ページ
+ アセットパイプライン
+ きれいなURL
+ LiveReload
+ ブログ機能

# 詳細 #

## はじめに ##

### インストール ###

    $ rvm gemset create middle_man
    $ rvm use ruby-1.9.3-p392@middle_man
    $ gem install middleman

### 新しいサイトの開発を始める ###

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

### 開発サイクル ###

1. サーバー起動

        $ cd introduction
        $ middleman server

1. ブラウザで確認

        http://localhost:4567/

1. 静的サイトのエクスポート

        $ cd introduction
        $ middleman build

### プロジェクトテンプレート ###

1. HTML5 Boilerplateプロジェクト作成

        $ middleman init introduction_boilerplate -T=html5

        $ tree introduction_boilerplate/
        introduction_boilerplate/
        ├── Gemfile
        ├── Gemfile.lock
        ├── config.rb
        └── source
            ├── 404.html
            ├── LICENSE.md
            ├── README.md
            ├── apple-touch-icon-114x114-precomposed.png
            ├── apple-touch-icon-144x144-precomposed.png
            ├── apple-touch-icon-57x57-precomposed.png
            ├── apple-touch-icon-72x72-precomposed.png
            ├── apple-touch-icon-precomposed.png
            ├── apple-touch-icon.png
            ├── crossdomain.xml
            ├── css
            │   ├── main.css
            │   └── normalize.css
            ├── favicon.ico
            ├── humans.txt
            ├── img
            ├── index.html.erb
            ├── js
            │   ├── main.js
            │   ├── plugins.js
            │   └── vendor
            │       ├── jquery-1.8.0.min.js
            │       └── modernizr-2.6.1.min.js
            ├── layouts
            │   └── layout.erb
            └── robots.txt

1. モバイルテンプレートの作成

        $ mkdir introduction_boilerplate/.middleman
        $ cd introduction_boilerplate/.middleman/
        $ middleman init introduction_mobile_boilerplate -T=mobile
        $ cd ..
        $ mv introduction_mobile_boilerplate/ .middleman/
        $ tree .middleman/
        .middleman/
        └── introduction_mobile_boilerplate
            ├── Gemfile
            ├── Gemfile.lock
            ├── config.rb
            └── source
                ├── 404.html
                ├── README.markdown
                ├── crossdomain.xml
                ├── css
                │   └── style.css
                ├── humans.txt
                ├── img
                │   ├── h
                │   │   ├── apple-touch-icon.png
                │   │   └── splash.png
                │   ├── l
                │   │   ├── apple-touch-icon-precomposed.png
                │   │   ├── apple-touch-icon.png
                │   │   └── splash.png
                │   └── m
                │       └── apple-touch-icon.png
                ├── index.html
                ├── js
                │   ├── libs
                │   │   ├── modernizr-custom.js
                │   │   └── respond.min.js
                │   ├── mylibs
                │   │   └── helper.js
                │   ├── plugins.js
                │   └── script.js
                ├── robots.txt
                ├── sitemap.xml
                ├── test
                │   ├── index.html
                │   ├── qunit
                │   │   ├── qunit.css
                │   │   └── qunit.js
                │   └── tests.js
                └── tools
                    ├── googleanalyticsformobile
                    │   ├── Readme.PDF
                    │   ├── aspx
                    │   │   ├── aspx1.snippet
                    │   │   ├── aspx2.snippet
                    │   │   ├── ga.aspx
                    │   │   └── sample.aspx
                    │   ├── jsp
                    │   │   ├── ga.jsp
                    │   │   ├── jsp1.snippet
                    │   │   ├── jsp2.snippet
                    │   │   └── sample.jsp
                    │   ├── php
                    │   │   ├── ga.php
                    │   │   ├── php1.snippet
                    │   │   ├── php2.snippet
                    │   │   └── sample.php
                    │   └── pl
                    │       ├── ga.pl
                    │       ├── perl1.snippet
                    │       ├── perl2.snippet
                    │       └── sample.pl
                    ├── mobile-bookmark-bubble
                    │   ├── COPYING
                    │   ├── bookmark_bubble.js
                    │   ├── example
                    │   │   ├── example.html
                    │   │   └── example.js
                    │   └── images
                    │       ├── arrow.png
                    │       ├── close.png
                    │       ├── generate_base64_images
                    │       └── icon_calendar.png
                    └── wspl
                        ├── README
                        ├── databasefactory.js
                        ├── dbworker.js
                        ├── dbworker_test.html
                        ├── dbworkerstarter.js
                        ├── dbwrapper_gears.js
                        ├── dbwrapper_gears_test.html
                        ├── dbwrapper_html5.js
                        ├── dbwrapper_html5_test.html
                        ├── dbwrapperapi.js
                        ├── dbwrapperapi_test.html
                        ├── gears_resultset.js
                        ├── gears_resultset_test.html
                        ├── gears_transaction.js
                        ├── gears_transaction_test.html
                        ├── gearsutils.js
                        ├── gearsutils_test.html
                        ├── global_functions.js
                        └── simplenotes
                            ├── index.html
                            ├── simplenotes.js
                            ├── styles.css
                            └── template.js        

## テンプレート ##

### レイアウト ###

introduction/source/layouts/layout.erb

    <html>
      <head>
        <title>私のサイト</title>
      </head>
      <body>
        <%= yield %>
      </body>
    </html>

introduction/source/index.html.erb

    <h1>Hello World</h1>

### カスタムレイアウト ###

introduction/source/layouts/admin.erb

    <html>
      <head>
        <title>管理エリア</title>
      </head>
      <body>
        <%= yield %>
      </body>
    </html>

introduction/config.rb

    page "/admin/*", :layout => "admin"

introduction/source/login.html.erb

    <h1>Login</h1>
    <form>
      <input type="text" placeholder="Email">
      <input type="password">
      <input type="submit">
    </form>

introduction/config.rb

    page "/login.html", :layout => "admin"

ブラウザで確認

    http://localhost:4567/login.html

### パーシャル ###

introduction/source/_footer.erb

    <footer>
      Copyright 2011
    </footer>

introduction/source/layouts/layout.erb

    <html>
      <head>
      <title>私のサイト</title>
      </head>
      <body>
        <%= yield %>
        <%= partial "footer" %>            
      </body>
    </html>

introduction/source/layouts/admin.erb

    <html>
      <head>
        <title>管理エリア</title>
      </head>
      <body>
        <%= yield %>
        <%= partial "footer" %>      
      </body>
    </html>


## Frontmatter ##

## 動的ページ ##

## アセットパイプライン ##

## きれいなURL ##

## LiveReload ##

## ブログ機能 ##

# 参照 #

[MiddleMan](http://middlemanapp.com/)

[MiddleMan日本語ページ](http://middlemanjp.github.io/)
