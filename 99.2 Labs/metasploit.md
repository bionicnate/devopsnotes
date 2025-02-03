https://ianmuchina.com/docker-lab/
---
docker-compose up -d
tty: true # activates interactive shell


sudo docker run \
    --name parrot \
    -it \
    --hostname parrot \
    --network vulnerable \
    --ip="10.0.0.2" \
    --env DISPLAY=$DISPLAY \
    -v /dev/shm:/dev/shm \
    --device /dev/snd \
    --device /dev/dri \
    --mount type=bind,src=/tmp/.X11-unix,dst=/tmp/.X11-unix \
    parrotsec/security:latest \
    /bin/bash
    
Use this command to restart the parrot OS container after a reboot.
    sudo docker start -a parrot

docker run \
    -it \
    --network vulnerable \
    --ip="10.0.0.3" \
    --name metasploitable \
    --hostname metasploitable2 \
    tleemcjr/metasploitable2 \
    bash

docker run -d \
    --name juiceshop \
    --network vulnerable \
    --ip="10.0.0.6" \
    bkimminich/juice-shop
    
docker run  -d \
    --name webgoat \
    --network vulnerable \
    --ip="10.0.0.4" \
    -e TZ=$(cat /etc/timezone) \
    webgoat/goatandwolf