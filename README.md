# Laravel set up using Docker

## Clone Project
git clone <url>
## Change origin url to your remote project url
git remote set-url origin <new url>
## create laravel project
docker-compose run --rm composer create-project --prefer-dist laravel/laravel .
## change env file(s) default is homestead
In /src/.env, change db info to match /env/mysql.env
MYSQL_DATABASE = DB_DATABASE
MYSQL_USER = DB_USERNAME
MYSQL_PASSWORD = DB_PASSWORD
MYSQL_ROOT_PASSWORD = DB_PASSWORD
## start up the project
docker-compose up -d --build server

## stop project
docker-compose down

## Connecting mysql container to external database gui
Publish internal port to whatever port number you want to use outside of docker
  mysql:
    image: mysql:5.7
    platform: linux/amd64
    env_file:
      - ./env/mysql.env
    ports:
      - "YOUR PORT NUMBER HERE:3306"

## Connection refused when running artisan migration
docker-compose run --rm artisan cache:clear

docker-compose run --rm artisan config:cache

docker-compose run --rm artisan view:clear

docker-compose run --rm artisan route:clear

docker-compose run --rm artisan config:clear
