FROM alpine:latest

RUN set -x \
    && addgroup -g 101 -S nginx \
    && adduser -S -D -H -u 101 -h /var/cache/nginx -s /sbin/nologin -G nginx -g nginx nginx \
    && apk -U upgrade\
    && apk add nginx vim bash curl \
    && mkdir -p /www/data \
    && mkdir -p /run/nginx \
    && chown -R nginx:nginx /var/lib/nginx \
    && chown -R nginx:nginx /www/data \
#  index.html
    && echo "Default web page" > /www/data/index.html \ 
# Forward request and error logs to docker log collector
# variables.
    && chown -R nginx:nginx /var/log/nginx \
    && ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

COPY nginx.conf /etc/nginx/

EXPOSE 80

STOPSIGNAL SIGTERM

CMD ["nginx", "-g", "daemon off;"]