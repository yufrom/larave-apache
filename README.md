## ソースのダウンロード
- 適当な作業ディレクトリにて、ソースをcloneする。
```
git clone https://github.com/yufrom/larave-apache.git
```

## Postgres用マウントコンテナ作成（Windows対応）
```
docker volume create --name test_db
```

## コンテナの起動
```
docker-compose up -d
```

## laravelプロジェクトの開始
```
docker-compose exec web composer install
cp src/.env.example src/.env
docker-compose exec web php artisan key:generate
```

## mySQLへの接続テスト
- `.env`ファイルを開き、以下のように修正
```
DB_CONNECTION=mysql
DB_HOST=mysql-host
DB_PORT=3306
DB_DATABASE=test_db
DB_USERNAME=docker
DB_PASSWORD=docker
```

## postgresへの接続テスト
- `.env`ファイルを開き、以下のように修正
```
DB_CONNECTION=pgsql
DB_HOST=postgres-host
DB_DATABASE=test_db
DB_USERNAME=postgres
DB_PASSWORD=postgres
```

## ログインテスト
- 上記「mysqlへの接続テスト」または、「postgresへの接続テスト」の設定を行う。
```
docker-compose exec web php artisan make:auth
```

## マイグレーション
```
docker-compose exec web php artisan migrate
```
