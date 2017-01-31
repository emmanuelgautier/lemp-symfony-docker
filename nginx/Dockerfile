FROM nginx:1.11-alpine

ADD nginx.conf /etc/nginx/
ADD *.conf /etc/nginx/conf.d/*.conf
ADD sites/* /etc/nginx/sites-enabled/

CMD ["nginx"]

EXPOSE 80 443
