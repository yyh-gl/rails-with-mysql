# 参考サイト
[参考サイト1](https://arrown-blog.com/rails-mysql/#scaffold)と[参考サイト2](http://ruby-rails.hatenadiary.com/entry/20150314/1426332751)にお世話になりました

# 手順（Development環境）
1. 「config/database.yml」にmysqlに関する情報を記載する

```yml
default: &default
  adapter: mysql2
  encoding: utf8
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: <%= ENV['RAILS_MYSQL_USER'] %>
  password: <%= ENV['RAILS_MYSQL_PASSWORD'] %>
  socket: /tmp/mysql.sock

development:
  <<: *default
  database: mysql_development

test:
  <<: *default
  database: mysql_test

production:
  <<: *default
  database: <%= ENV['DB_NAME'] %>
  username: <%= ENV['DB_USERNAME'] %>
  password: <%= ENV['DB_PASSWORD'] %>
  host:     <%= ENV['DB_HOSTNAME'] %>
  port:     <%= ENV['DB_PORT'] %>
```

2. mysqlサーバを起動する

```zsh
$ mysql.server start
```

3. 「config/database.yml」に応じてデータベース作成（database: <作りたいデータベース名>）

```zsh
$ rails db:create
```

4. Rails＋Scaffoldでモデル（テーブル）を作成

```zsh
$ rails generate scaffold books title:string content:string
$ rails db:migrate
```

5. Railsサーバを起動して確認 -> 「http://localhost:3000/books」


# 手順（Production環境）

[参考サイト2](http://ruby-rails.hatenadiary.com/entry/20150314/1426332751)どおりにやればOK