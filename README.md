# nextcloud
```code
version: '3.8'

services:
  db:
    image: mariadb
    restart: always
    command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW --innodb-file-per-table=1 --skip-innodb-read-only-compressed
    env_file: .env
    environment:
      - MYSQL_DATABASE=nextclouddb
    volumes:
      - .dbvol:/var/lib/mysql

  nextcloud:
    depends_on:
    - db
    image: nextcloud
    restart: always
    env_file: .env
    environment:
      - MYSQL_PASSWORD=$MYSQL_PASSWORD
      - MYSQL_DATABASE=nextclouddb
      - MYSQL_USER=$MYSQL_USER
      - MYSQL_HOST=db
    ports:
      - 8080:80 #Port change
    volumes:
      - ./nchtml:/var/www/html
      - ./ncapps:/var/www/html/apps
      - ./ncconfig:/var/www/html/config
      - /nextcloud/data:/var/www/html/data
```
###
how to create .env file https://www.digitalocean.com/community/tutorials/how-to-install-wordpress-with-docker-compose
###
