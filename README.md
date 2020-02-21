docker_cakephp3
===

## インストール・コンテナの立ち上げ

```
$ git clone git@github:edo1z/docker_cakephp3.git
$ cd docker_cakephp3
$ docker-compose up -d
```

## WEBサーバのbashを起動

```
$ ./bash.sh web

# php -v
# apache2 -v
# composer
```

- PHP7.2.11とApache2.4.25が入っています。
- composerも利用可能です。
- composer updateやマイグレーションコマンド等はこちらで実施します。

## DBサーバのbashを起動

```
$ ./bash.sh db

# mysql -uroot -ppassword
```

- MariaDB 10.3.22が入っています。
- db1という名前のdatabaseが自動で作成されています。

## CakePHP3のデータベース設定

```
export DATABASE_URL="mysql://root:password@db:3306/db1?encoding=utf8mb4&timezone=Asia/Tokyo&cacheMetadata=true&quoteIdentifiers=false&persistent=false"
```

## Navicat等のデータベース設定

- Host => `localhost`
- Port => `3307`
- User => `root`
- Password => `password`

## （参考）DebugKitを無効にする方法

- DebugKitが有効な場合、非常に動きが遅い場合があります。
- デバッグ環境でも無効にするには、`src/Application.php` の49行目付近を下記のようにコメントアウトします。

```src/Application.php
48 if (Configure::read('debug')) {
49    //$this->addPlugin(\DebugKit\Plugin::class);
50 }
```

## メール送信テストの方法

- 本当のメール送信は出来ません。
- メール送信テストは、[MailHog](https://github.com/mailhog/MailHog)を使います。
- CakePHP3のメール送信設定を調整して開発時はMailHogに送信するようにする予定です。


