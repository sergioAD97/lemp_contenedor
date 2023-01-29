# Docker compose with MariaDB, nginx, php-fpm and phpmyadmin

## Used images

1. [MariaDB](https://hub.docker.com/_/mariadb/)
2. [Nginx](https://hub.docker.com/_/nginx/)
3. [php-fpm](https://hub.docker.com/r/nanoninja/php-fpm/)
4. [phpmyadmin](https://hub.docker.com/r/phpmyadmin/phpmyadmin/)

## Environment variables

See .env file

```
# Nginx
NGINX_HOST=localhost
HTTP_PORT=30080
HTTPS_PORT=30443

# PhpMyAdmin
PHPMYADMIN_PORT=38080

# MySQL
MARIADB_VERSION=10.3.10
MYSQL_PORT=33306
MYSQL_ROOT_PASSWORD=root
MYSQL_HOST=mysql
MYSQL_DATABASE=test
MYSQL_USER=test
MYSQL_PASSWORD=test
```

## User commands

Up containers
```
docker-compose up -d
```

See containers and exposed ports

```
docker container ls
```

Stop and remove containers
```
docker stop mysql && docker rm mysql
docker stop phpmyadmin && docker rm phpmyadmin
docker stop nginx && docker rm nginx
docker stop php-fpm && docker rm php-fpm
```

Connect to mysql from localhost
```
mysql -u root -p -h 127.0.0.1 --port $MYSQL_PORT
```

Connect to mysql from another container
```
MYSQL_CONTAINER_IP=$(docker container inspect mysql --format "{{.NetworkSettings.IPAddress}}"")

docker run -it mariadb mysql -h $MYSQL_CONTAINER_IP --port 3306 -u root -p
```

  or

```
docker run --network dockernginxphpmysql_docker-network -it mariadb mysql -h mysql --port 3306 -u root -p
```