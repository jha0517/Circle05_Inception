# use debian as the base image
FROM debian:buster

# install NGINX and other dependencies
RUN apt-get update -y 
RUN apt-get install -y nginx
RUN apt-get install -y vim
RUN apt-get install -y curl
RUN mkdir -p /etc/nginx/ssl
RUN apt-get install -y openssl

# 1)create a directory to store certificates and keys 2)generate the keys
# req => primarily creates and processes certificate requests
# -x509 => this option outputs a self signed certificate instead of a certificate request. 
RUN openssl req -x509 -nodes -out /etc/nginx/ssl/inception.crt -keyout /etc/nginx/ssl/inception.key -subj "/C=FR/ST=IDF/L=Paris/O=42/OU=42/CN=hyujung.42.fr/UID=hyujung"

# copy the provided config file to the container
RUN mkdir -p /var/run/nginx
COPY ./conf/nginx.conf /etc/nginx/nginx.conf

# FOR THE NGINX.CONF FILE, WE NEED TO GIVE PERMISSION AND OWENERSHIP.
RUN chmod 755 /var/www/html
# CHOWN -> CHANGE OWNERSHIP OF /VAR/WWW/HTML TO WWW-DATA:WWW-DATA. WHY? TO ENSURE THAT NGINX CAN READ AND SERVE THE FILES STORED IN THAT DIRECTORY, SUCH AS THE WORDPRESS FILES THAT WILL BE SERVED BY THE CONTAINER.
RUN chown -R www-data:www-data /var/www/html

# CMD : SETS THE DEFAULT COMMAND TO BE RUN WHEN A CONTAINER IS STARTED FROM THE DOCKER IMAGE.
# nginx -g : START NGINX, -G -> SHOULD BE EXECUTED WHEN THE SERVER STARTS UP.
# daemon off : TELLS NGINX TO RUN IN THE FOREGROUND, RATHER THAN AS A BACKGROUND DAEMON.
#              WHY? IT ALLOWS THE CONTAINER TO STAY RUNNING AS LONG AS THE NGINX SERVER IS RUNNING. IF NGINX WERE TO RUN IN THE BACKGROUND, THE CONTAINER WOULD EXIT AS SOONS AS THE NGINX PROCESS FINISHED.
CMD ["nginx", "-g", "daemon off;"]

