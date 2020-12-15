FROM alpine:edge
ARG SERVER_NAME
ARG PROJECT_NAME

LABEL maintainer="Mehrdad Khoddami <khoddami.me@gmail.com>"

RUN apk add --update --no-cache nginx

COPY docker/nginx/nginx.conf /etc/nginx/
COPY docker/nginx/symfony.conf /etc/nginx/conf.d/
		
COPY etc/aliases.sh /etc/profile.d/aliases.sh

RUN echo "upstream php-upstream { server php:9001; }" > /etc/nginx/conf.d/upstream.conf
RUN sed "/server_name symfony.localhost;/c\	server_name ${SERVER_NAME};" -i /etc/nginx/conf.d/symfony.conf
RUN sed "/root \/var\/www\/symfony\/public;/c\	root \/var\/www\/${PROJECT_NAME}\/public;" -i /etc/nginx/conf.d/symfony.conf

RUN adduser -D -g '' -G www-data www-data

CMD ["nginx"]

EXPOSE 80
EXPOSE 443