FROM nginx
WORKDIR /home/

USER root
COPY ./nginx.conf /etc/nginx/nginx.conf
COPY main.c .

RUN apt-get update 
RUN apt-get install -y libfcgi-dev spawn-fcgi gcc 

ENTRYPOINT  gcc main.c -lfcgi -o main && \
            spawn-fcgi -p 8080 ./main && \
            nginx -g 'daemon off;' 