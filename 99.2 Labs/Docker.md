docker pull nginx:latest

docker run -it nginx

Find last created container 
: docker ps -n 1

### Adding Persistence

docker run -itd \                                       
>   --name nginx-nobindmount \
>   -p 8080:80 nginx:latest

➞  echo -e "\nhttp://$(cat /ab/hostname):8080\n"           

➞  docker run -itd \                                       
>   --name nginx-bindmount \
>   -v /ab/labs/containers/basics:/usr/share/nginx/html \
>   -p 8081:80 \
>   nginx:latest

➞  echo -e "\nhttp://$(cat /ab/hostname):8081\n"           

➞  docker rm -f nginx-nobindmount nginx-bindmount          
nginx-nobindmount
nginx-bindmount

### Adding Networks

➞  docker network create external                          
➞  docker network create database                          
➞  docker network ls                                       

➞  docker run -itd \                                       
>   --name nginx1 \
>   -v nginx1:/usr/share/nginx/html \
>   -p 8080:80 \
>   --network="external" \
>   alphabravoio/ubuntu-nginx:latest

➞  docker network connect database nginx1                  

➞  docker container inspect nginx1 | jq '.[].NetworkSettings.Networks'

➞  docker run -itd \                                       
>   --name apache1 \
>   -v /ab/labs/tmp/apache1:/var/www/html \
>   -p 8081:80 \
>   --network="external" \
>   alphabravoio/ubuntu-apache2:latest

➞  docker run -itd \                                       
>   --name mysql1 \
>   -v mysql1:/var/lib/mysql \
>   --network="database" \
>   -e MYSQL_ROOT_PASSWORD=mysecretpassword \
>   alphabravoio/ubuntu-mysql:latest

➞  docker ps -n 3 --format "{{.Names}}"                    

➞  docker exec -it nginx1 /bin/bash                        

### Starting Wordpress Docker

➞  review /ab/labs/containers/compose/docker-compose.yml   
   1   services:
   2     mariadb:
   3       image: docker.io/bitnami/mariadb:10.3
   4       volumes:
   5         - 'mariadb_data:/bitnami/mariadb'
   6       environment:
   7         - MARIADB_ROOT_USER=wordpress
   8         - MARIADB_ROOT_PASSWORD=yourpassword
   9         - MARIADB_DATABASE=wordpress
  10       networks:
  11         - database_net
  12   
  13     wordpress:
  14       image: docker.io/bitnami/wordpress:5
  15       ports:
  16         - '8080:8080'
  17         - '8443:8443'
  18       volumes:
  19         - 'wordpress_data:/bitnami/wordpress'
  20       depends_on:
  21         - mariadb
  22       environment:
  23         - WORDPRESS_DATABASE_HOST=mariadb
  24         - WORDPRESS_DATABASE_PORT_NUMBER=3306
  25         - WORDPRESS_DATABASE_USER=wordpress
  26         - WORDPRESS_DATABASE_PASSWORD=yourpassword
  27         - WORDPRESS_DATABASE_NAME=wordpress
  28         - WORDPRESS_BLOG_NAME=AB_Training_Docker_Compose
  29       networks:
  30         - external_net
  31         - database_net
  32   
  33   volumes:
  34     mariadb_data:
  35       driver: local
  36     wordpress_data:
  37       driver: local
  38   
  39   networks:
  40     external_net:
  41       driver: bridge
  42     database_net:
  43       driver: bridge

➞  docker compose -f /ab/labs/containers/compose/docker-compose.yml up -d

