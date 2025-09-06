FROM nginx:latest

RUN rm -rf /usr/share/nginx/html/*
COPY html/ /usr/share/nginx/html/
RUN chown -R www-data:www-data /usr/share/nginx/html

COPY default.conf /etc/nginx/conf.d/default.conf
COPY ssl.conf /etc/nginx/conf.d/ssl.conf
COPY nginx.conf /etc/nginx/nginx.conf

COPY ssl/nginx.crt /etc/nginx/
COPY ssl/nginx.key /etc/nginx/
