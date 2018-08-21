# hello-ruby-app

## Info
* Heroku Simple Tutorial
* 超初歩的な Heroku x ruby

## Basic Component
```
.
|-- .gitignore
|-- Procfile        # heroku app 処理管理ファイル
|-- app.json        # heroku app パッケージ管理ファイル
|-- Gemfile         # ruby パッケージ管理ファイル, 構成管理用
|-- Gemfile.lock    # ruby パッケージ管理ファイル, 最新バージョンの保持用
|-- .ruby-version   # rbenv バージョン管理ファイル
|-- vendor          # 外部スクリプト用ディレクトリ, bundle で管理
|   `-- bundle
|       `-- ruby
|           `-- *.*.*
|               |-- bin
|               |-- ...
|               `-- specifications
|-- config.ru       # main script
`-- README.md       # this
```

## How to startup?
1. `bundle` で ruby プロジェクトを初期化

    ```sh
    $ bundle init
    ```

2. `Gemfile`を編集，ruby のバージョンと rack の依存関係を指定

    ```diff
    + ruby "2.2.3"  # example
    + gem "rack"
    ```

3. `bundle`でパッケージをインストール

    ```sh
    $ bundle install --path vendor/bundle
    ```

4. `config.ru`を作成，リクエストに "Hello World" で応答

    ```sh
    $ touch config.ru
    ```

    ```ruby
    run proc { [ 200, {}, ["Hello World"] ] }
    ```


5. `.gitignore`を作成，`vendor/`を追加

    ```bash
    $ echo "vendor/" > .gitignore
    ```

6. git リポジトリと heroku app を作成，リモートに push する

    ```bash
    $ git init
    $ git add . && git commit -m "[$MESSAGE]"
    $ heroku app create [$APP_NAME]
    $ git push heroku master
    ```

7. `curl`および`heroku open`で heroku app を確認

    ```bash
    $ curl https://[$APP_NAME].herokuapp.com
    $ heroku open
    ```

Note
* ruby のバージョン管理ツール`rbenv`を利用する場合
    1. 指定のバージョンをインストール

        ```sh
        $ rbenv install -l      # インストール可能なバージョン一覧
        $ rbenv install *.*.*
        ```

    2. ローカルの ruby のバージョンを切り替え

        ```sh
        # 実行後，`.ruby-version`というファイルが自動で作成される
        $ rbenv local *.*.*
        ```

    3. `bundle`でインストール

        ```sh
        $ bundle install --path vendor/bundle
        ```


------

## Ref
* Ruby アプリをクラウドにデプロイ・運用・スケール - Heroku, [https://jp.heroku.com/ruby](https://jp.heroku.com/ruby)