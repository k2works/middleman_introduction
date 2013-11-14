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



## テンプレートヘルパ ##

### リンクヘルパ ###
index.html.erb
  
    <%= link_to 'About','/about.html' ,relative: true %>

config.rb

    set :relative_links, true

### 出力ヘルパ ###
layout.erb

    <% if content_for?(:assets) %>
      <div><%= yield_content :assets %></div>
    <% end %>    
        
index.html.erb

    <% content_for :assets do %>
      <%= stylesheet_link_tag 'index','custom' %>
    <% end %>

### タグヘルパ ###
+ tag
+ content_tag
+ input_tag

    index.html.erb

        <%= tag :img, src: "http://lorempixel.com/400/200/" %>
        <br>
        <% content_tag :p, class: "stuff" do %>
        こんにちは
        <% end %>
        <br>
        <%= input_tag :text, class: "demo" %>
        <br>
        <%= input_tag :password, value: "secret",class: "demo" %>

### アセットヘルパ ###
asset.html.erb

    <html>
      <head>
        <%= stylesheet_link_tag 'layout' %>
        <%= javascript_include_tag 'application' %>
        <%= favicon_tag 'images/favicon.png' %>
      </head>
      <body>
        <p><%= link_to 'Blog', '/blog', class: 'example' %></p>
        <p>Mail me at <%= mail_to 'fake@faker.com',"Fake Email Link",cc: "test@demo.com" %></p>
        <p><%= image_tag 'padrino.png', width: '35',class:'logo' %></p>
      </body>
    </html>


### フォームヘルパ ###

### フォーマットヘルパ ###
+ escape_html
+ distance_of_time_in_words
+ time_ago_in_words
+ js_escape_html

    format.html.erb

        <%= simple_format("hellow\nworld") %>
        <%= pluralize(2,'人') %>
        <br>
        <%= word_wrap('Once upon a time', line_width: 8 ) %>
        <br>
        <%= truncate("Once upon a time in world far far away", length: 16) %>
        <br>
        <%= truncate_words("Once upon a time in world far far away", length: 4) %>
        <br>
        <%= highlight('Lorem dolor sit', 'dolor') %>

### ダミーテキスト ###
+ dummy.html.erb

        <%= lorem.sentence %>
        <br>
        <%= lorem.words 5 %>
        <br>
        <%= lorem.word %>
        <br>
        <%= lorem.paragraphs 10 %>
        <br>
        <%= lorem.paragraph %>
        <br>
        <%= lorem.date %>
        <br>
        <%= lorem.name %>
        <br>
        <%= lorem.first_name %>
        <br>
        <%= lorem.last_name %>
        <br>
        <%= lorem.email %>
        <br>
        <%= tag :img, src: lorem.image('300x400') %>
        <%= tag :img, src: lorem.image('300x400',background_color: '333',color: 'fff') %>
        <%= tag :img, src: lorem.image('300x400',random_color: true) %>
        <%= tag :img, src: lorem.image('300x400',text:'blah') %>

### ページクラス ###
+ layout/layout.erb

        <body class="<%= page_classes %>">

### カスタム定義ヘルパ ###
+ config.rb

        helpers do
          def some_method
            #...何らかの処理を追加...
          end
        end

+ 外部モジュール

        $ mkdir lib
        $ touch lib/custom_helpers.rb

+ lib/custom_helpers.rb

        module CustomHelpers
          def some_method
            # ..do something here...
          end
        end

+ config.rb

        require "lib/custom_helpers"
        helpers CustomHelpers

+ より簡単な方法

        $ mkdir helpers
        $ cp lib/custom_helpers.rb helpers/

## Frontmatter ##
+ YAML

        ---
        layout: "layout"
        my_list:
          - one
          - two
          - three
        ---

        <h1>YAMLリスト</h1>
        <o1>
          <% current_page.data.my_list.each do |f| %>
            <li><%= f %></li>
          <% end %>
        </ol>

+ JSON

        ;;;
        "layout": "layout",
        "my_list": [
          "one",
          "two",
          "three"
        ]
        ;;;

        <h1>JSONリスト</h1>
        <o1>
          <% current_page.data.my_list.each do |f| %>
            <li><%= f %></li>
          <% end %>
        </ol>
  
## 動的ページ ##

### Proxyの定義 ###

    $ mkdir source/about
    $ touch source/about/template.html.erb

+ about/template.html.erb

        ---
        layout: layout
        ---

        <h1>テンプレート</h1>

+ config.rb

        ["tom","dick","harry"].each do |name|
          proxy "/about/#{name}.html","/about/template.html", locals: {person_name: name}, ignore: true
        end

        ignore "/about/template.html"


## アセットパイプライン ##

## きれいなURL ##

## LiveReload ##

## ブログ機能 ##

# 参照 #

[MiddleMan](http://middlemanapp.com/)

[MiddleMan日本語ページ](http://middlemanjp.github.io/)

[シリーズMiddleman で静的 Web サイトを超速プロトタイピング](http://dev.classmethod.jp/series/middleman-%E3%81%A7%E9%9D%99%E7%9A%84-web-%E3%82%B5%E3%82%A4%E3%83%88%E3%82%92%E8%B6%85%E9%80%9F%E3%83%97%E3%83%AD%E3%83%88%E3%82%BF%E3%82%A4%E3%83%94%E3%83%B3%E3%82%B0/)
