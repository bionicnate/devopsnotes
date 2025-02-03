Personal Media Server and Cloud

	1. Docker

	2. Portainer
	   1) docker pull portainer/portainer-ce
	   2) docker volume create portainer_data
	   3) docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce

	3. Plex & Nextcloud
      1> docker pull linuxserver/plex
         1. docker run -d \
  --name=plex \
  --net=host \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Etc/UTC \
  -e VERSION=docker \
  -e PLEX_CLAIM= `#optional` \
  -v /path/to/plex/library:/config \
  -v /path/to/tvseries:/tv \
  -v /path/to/movies:/movies \
  --restart unless-stopped \
  lscr.io/linuxserver/plex:latest

      2> docker pull nextcloud
      3> docker run -d -p 8080:80 nextcloud
      4> docker run -d \
-v nextcloud:/var/www/html \
nextcloud
	   5> docker run -d \
-v db:/var/lib/mysql \
mariadb:10.6
		
	1. Docker Compose
		1) write docker-compose.yaml		
		2) docker compose up -d




	
