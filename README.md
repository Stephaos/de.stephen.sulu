# Sulu CMS with Docker Setup

## Installation
__Linux:__
```
docker-compose up -d
docker-compose exec php-fpm bin/adminconsole sulu:build dev
docker-compose exec php-fpm chmod -R 777 /var/www/app
docker-compose down
```

#### Enjoy