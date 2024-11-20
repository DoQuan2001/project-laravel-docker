# Sử dụng image PHP 8.3-fpm
FROM php:8.3-fpm

# Cài đặt các dependencies cần thiết cho pdo_mysql


# Cài đặt các dependencies cần thiết cho pdo_mysql
RUN apt-get update && apt-get install -y \
    default-libmysqlclient-dev \
    && docker-php-ext-install pdo pdo_mysql

# Cài đặt thư viện và extension khác nếu cần thiết
WORKDIR /var/www/html
