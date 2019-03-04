# Docker image for Grafana for Raspberry Pi
## Link https://cloud.docker.com/repository/docker/churruscat/grafana-rpi
  
## Run 
docker run -ti -p 3000:3000 -p 9001:9001 churruscat/grafana    
  Exposes Port 3000 (grafana)  

## Running with persistence  
Local directories / External Configuration  
Alternatively you can use volumes to make the changes persistent and change the configuration.  
mkdir -p /IOTserver/grafana/  

\# place your grafana.ini in /IOTserver/grafana 
\# NOTE: You have to change the permissions of the directories   
\# to allow the user to read/write to data and log and read from   
\# config directory   
\# For TESTING purposes you can use chmod -R 777 /IOTserver/grafana/*   
\# Better use "-u" with a valid user id on your docker host   

docker run -ti -p 1883:1883 -p 9001:9001 \\   
-v /IOTserver/grafana:/etc/grafana:rw \\   
-v /IOTserver//grafana:/var/lib/grafana:rw \\   
Volumes: /var/lib/grafana, /etc/grafana   


## Running with Docker-compose: 
  grafana:   
    container_name: grafana   
    image: churruscat/grafana-rpi   
    ports:   
      - 3000:3000   
    volumes:   
      - /IOTServer/grafana:/etc/grafana:rw   
      - /IOTServer/grafana:/var/lib/grafana:rw   
    restart: on-failure   
    depends_on:   
     \# if visualizing influxdb data   
      influxdb:    
      condition: service_healthy   

