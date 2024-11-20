# APACHE + PHP + COMPOSER + MYSQL + PHPMYADMIN BY DOCKER.

## I. CẤU TRÚC THƯ MỤC.

### cấu trúc thư mục:

```
.
├── 1_apache 
├── 2_php
├── docker-compose.yml  # file compose này gồm 5 service: apache, php-fpm, mysql, composer và phpmyadmin
└── laravel-app  #project laravel của bạn.

```

### 5 cái service trong file docker-compose:

- apache: websever.
- php-fpm: để chạy php core.
- mysql: chạy db.
- composer: nạp thư viện cho laravel.
- phpmyadmin: giao diện web cho mysql.


## II. HƯỚNG DẪN SỬ DỤNG.

### 2.1. BƯỚC 1: CHẠY CÁC CONTAINER.

`docker-compose up -d`: lệnh chạy.

NẾU BẠN CÓ CHỈNH SỬA CẤU HÌNH NÀO ĐÓ Ở 1 SỐ FILE CONFIG, DOCKERFILE CẦN BUILD TỪ ĐẦU THÌ CHẠY LỆNH: `docker-compose up --build`

### 2.2. TẠO PROJECT LARAVEL.

TA CẦN TRUY CẬP VÀO CONTAINER COMPOSER ĐỂ TẠO PROJECT.

`docker exec -it composer-container /bin/bash`: vào container composer.

SAU KHI VÀO CONTAINER CẦN CHẠY LỆNH SAU ĐỂ TẠO PROJECT.

`composer create-project --prefer-dist laravel/laravel .`: lệnh tạo project.

**KẾT HỢP 2 LỆNH TRÊN NẾU K MUỐN VÀO CONTAINER:** `docker exec -it composer-container bash -c "composer create-project --prefer-dist laravel/laravel ." `

LÚC NÀY, TA THẤY SOURCE CODE ĐÃ Ở THƯ MỤC `LARAVEL-APP`.

### 2.3. KẾT NỐI PROJECT VỚI DB.

TRUY CẬP VÀO FILE `.EVN` TRONG THƯ MỤC `LARAVEL-APP`. VÀ CHỈNH SỬA NHƯ SAU:

```
DB_CONNECTION=mysql
DB_HOST=mysql # ten service của container mysql trong file docker-compose.
DB_PORT=3306
DB_DATABASE=my_database
DB_USERNAME=user
DB_PASSWORD=userpassword

```

SAU ĐÓ, HÃY VÀO CONTAINER PHP ĐỂ CHẠY LỆNH TẠO LẠI CSDL:

`docker-compose exec php-fpm-container php artisan migrate`: vào container php-fpm.

`php artisan migrate`: lệnh tạo lại csdl.

**KẾT HỢP 2 LỆNH TRÊN NẾU K MUỐN VÀO CONTAINER:** `docker-compose exec php-fpm-container bash -c "php artisan migrate" `

TRUY CẬP `localhost:8089` để xem CSDL ĐÃ ĐƯỢC HÌNH THÀNH CHƯA NHA. TÊN CSLD LÀ `my_database`.


## III. KIỂM TRA.

TRUY CẬP `localhost:8088` để kiểm tra kết quả.


