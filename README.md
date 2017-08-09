# ER2: Docker Webapps
A simple image that is used for base webapps at ER2

## Setup:

1. Create a .env from the .env.dist file. Adapt it according to your Symfony application
    `nano .env`

    ```
    MYSQL_ROOT_PASSWORD=password
    MYSQL_DATABASE=database
    MYSQL_USER=user
    MYSQL_PASSWORD=password
    APP_NAME=new-app
    ```

2. Build/run containers with (with and without detached mode)
```
$ docker-compose build
$ docker-compose up -d
```

3. Prepare Symfony app

Either create a new one or drag your old one to the `symfony` folder.

i. Update app/config/parameters.yml
```
# symfony/app/config/parameters.yml
parameters:
    database_host: db
```

ii. Composer install & create database

```
$ docker-compose exec php bash
$ composer install
# Symfony3
$ sf3 doctrine:database:create
$ sf3 doctrine:schema:update --force
# Only if you have `doctrine/doctrine-fixtures-bundle` installed
$ sf3 doctrine:fixtures:load --no-interaction
```


