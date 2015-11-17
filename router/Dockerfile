# Set nginx base image
FROM nginx

# File Author / Maintainer
MAINTAINER Giles Dring <giles@dringtech.com>

RUN mkdir /etc/nginx/ssl
COPY ssl/ /etc/nginx/ssl
COPY nginx.conf /etc/nginx/nginx.conf
COPY sites/* /etc/nginx/sites-enabled/
