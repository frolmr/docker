FROM debian:11

COPY lab1.list /etc/apt/sources.list.d/

RUN apt update && \
    apt upgrade -y && \
    apt install -y nginx && \
    apt clean

RUN rm -rf /var/www/* && \
    mkdir -p /var/www/frol.pw/img

COPY index.html /var/www/frol.pw
COPY img.jpg /var/www/frol.pw/img

RUN chmod -R 754 /var/www/frol.pw

RUN useradd anton && \
    groupadd frolov && \
    usermod -g frolov anton

RUN chown -R anton:frolov /var/www/frol.pw

RUN sed -i 's/\/var\/www\/html;/\/var\/www\/frol.pw;/' /etc/nginx/sites-enabled/default && \
    sed -i 's/user www-data;/user anton;/' /etc/nginx/nginx.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
