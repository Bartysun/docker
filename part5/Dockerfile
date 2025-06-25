FROM nginx
WORKDIR /home/

COPY ./nginx.conf /etc/nginx/nginx.conf
COPY main.c .

RUN apt-get update; \ 
    apt-get install -y gcc spawn-fcgi libfcgi-dev; \
    chown -R nginx:nginx /etc/nginx/nginx.conf; \
    chown -R nginx:nginx /var/cache/nginx; \
    chown -R nginx:nginx /home; \
    touch /var/run/nginx.pid; \
    chown -R nginx:nginx /var/run/nginx.pid; \
    rm -rf /var/lib/apt/lists

USER nginx

HEALTHCHECK --interval=5m --timeout=3s \
CMD curl -f http://localhost/ || exit 1 
  

ENTRYPOINT  spawn-fcgi -p 8080 ./main && \
            nginx -g 'daemon off;' 
