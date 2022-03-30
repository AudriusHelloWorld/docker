FROM nginx:1.15.8-alpine

COPY ./servers/app.conf /etc/nginx/conf.d/app.conf
COPY ./nginx.conf /etc/nginx/nginx.conf

COPY . /var/www