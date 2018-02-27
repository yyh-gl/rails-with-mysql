# 参考サイト
[本記事](https://arrown-blog.com/rails-mysql/#scaffold)にお世話になりました

# 手順
1. 「config/database.yml」にmysqlに関する情報を記載する

```
default: &default
  adapter: mysql2
  encoding: utf8
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: 
  password: 
  socket: /tmp/mysql.sock

development:
  <<: *default
  database: mysql_development

test:
  <<: *default
  database: mysql_test

production:
  <<: *default
  database: mysql_production
```

2. mysqlサーバを起動する

```
$ mysql.server start
```

3. 「config/database.yml」に応じてデータベース作成（database: <作りたいデータベース名>）

```
$ rails db:create
```

4. Rails＋Scaffoldでモデル（テーブル）を作成

```
$ rails generate scaffold books title:string content:string
$ rails db:migrate
```

5. Railsサーバを起動して確認 -> 「http://localhost:3000/books」