# Docker Lnmp
## Introduce
* This is a simple and small Docker+Nginx+Php+Mysql+Phpmyadmin envirment

## Including
* Nginx alpine
* php 8 fpm alpine
* php 7.4 fpm alpine
* mysql 8
* phpmyadmin lastest (default run in http://localhost:8085)

## Build image
```
docker-compose build
```
## Start Up
```
docker-compose --profile php74 -d up
OR
docker-compose --profile php80 -d up
```
- If you start up php version different from last time ， you need to check nginx.conf <strong>fastcgi_pass</strong> path wheather the right service
- This will only start up Nginx PHP Mysql Phpmyadmin four services，if want start up other service need use
- ```
    docker-compose -d service_name up
    ```

## Exec something in nginx
```
docker exec -it nginx /bin/sh
```

## Exec something in php
```
docker exec -it php74 /bin/sh
docker exec -it php80 /bin/sh
```
## 快速重新Build後啟動
有更改設定檔時重啟
```
docker-compose --profile php80 up -d --no-deps --force-recreate --build
```

## 錯誤處理 
當所有設定或是PORT都沒有問題，但是不管怎麼打API或URL都只能看到NGINX 404時，很有可能是我裝了supervisor後，php-fpm服務不會自動起來，所以解法有:
* docker file 把supervisor相關的東西拔掉後重新build image 和 run 
* 進入使用的php container後，下指令"php-fpm"
