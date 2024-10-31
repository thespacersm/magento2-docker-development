# Magento2 docker development
Development Docker for Magento 2, not fast, just simple.

## Getting Started

Copy the `docker-compose.yml` and `.docker` folder to your Magento 2 root directory.

```bash
cp docker-compose.yml /path/to/magento2
cp -r .docker /path/to/magento2
```

Copy the environment file `.env.example` to `.env` and set the environment variables.

```bash
cat .env.example >> /path/to/magento2/.env
```

If you need to install it, you can run:

```bash
php bin/magento setup:install --db-host="mysql" --db-user="magento2" --db-name="magento2" --db-password="magento2" --search-engine=opensearch --opensearch-host="opensearch" --opensearch-port="9200" --opensearch-index-prefix="magento2" --session-save="redis" --session-save-redis-host="redis" --session-save-redis-port="6379" --session-save-redis-db=0     --session-save-redis-max-concurrency=20     --cache-backend=redis     --cache-backend-redis-server=redis     --cache-backend-redis-db=1     --cache-backend-redis-port=6379     --page-cache=redis     --page-cache-redis-server=redis     --page-cache-redis-db=2     --page-cache-redis-port=6379
```

Edit in app/etc/env.php the database configuration.

```php
<?php
return [
    'db' => [
        'table_prefix' => '',
        'connection' => [
            'default' => [
                'host' => 'mysql',
                'dbname' => 'magento2',
                'username' => 'magento2',
                'password' => 'magento2',
                'active' => '1'
            ]
        ]
    ]
];
```

Run the docker-compose command.

```bash
docker-compose up -d --build
```

Set the base url, for example if you are using `localhost` and port `8080` then the base url is `http://localhost:8080/`.

```bash
php bin/magento config:set -e  "web/unsecure/base_url" "http://localhost:8080/"
php bin/magento config:set -e  "web/secure/base_url" "http://localhost:8080/"
```

Set the opensearch configuration.

```bash
php bin/magento config:set -e  "catalog/search/opensearch_server_hostname" "opensearch"
```

Set the redis configuration.

```bash
php bin/magento setup:config: set --cache-backend=redis --cache-backend-redis-server=redis --cache-backend-redis-db=0

php bin/magento setup:config: set --page-cache=redis --page-cache-redis-server=redis --page-cache-redis-db=1

php bin/magento setup:config: set --session-save=redis --session-save-redis-host=redis --session-save-redis-log-level=3 --session-save-redis-db=2
```

Clear the cache.

```bash
php bin/magento cache:flush
```
