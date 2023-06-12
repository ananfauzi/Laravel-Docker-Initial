# Laravel-Docker-Initial
Initial docker file for new laravel project

# 1. Requirement
We assume docker and docker-compose already installed on your system.

# 2. How to use
a. Pull this repository
b. Inside your local machine create src/ directory
```
mkdir src
```
c. execute below script
```
docker compose up -d --build
docker compose exec php-server /bin/bash
composer create-project laravel/laravel .
php artisan migrate
php artisan serve
```
