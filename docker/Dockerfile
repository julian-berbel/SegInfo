FROM debian:wheezy

LABEL maintainer "opsxcq@strm.sh"

RUN apt-get update && \
    apt-get upgrade -y && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
    apache2 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

COPY packages /packages

RUN dpkg -i /packages/*

COPY vulnerable /usr/lib/cgi-bin/
COPY index.html /var/www
COPY .htaccess /usr/lib
COPY blocked.php /var/www
COPY default /etc/apache2/sites-available

RUN chown www-data:www-data /var/www/index.html
RUN ln -s /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/rewrite.load

EXPOSE 80

COPY main.sh /

ENTRYPOINT ["/main.sh"]
CMD ["default"]

