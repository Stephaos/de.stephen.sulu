FROM nginx:1.10.1

ENV APP_BASEDIR=/var/www/app

COPY ./docker/nginx/nginx.conf /etc/nginx/conf.d/default.conf

COPY ./ $APP_BASEDIR/

WORKDIR $APP_BASEDIR/