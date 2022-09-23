FROM centos:7

RUN yum install -y httpd mod_ssl \
    php73 php74 php{73,74}-intl php{73,74}-soap php{73,74}-gd php{73,74}-mbstring php{73,74}-xml \
    php{73,74}-mcrypt php{73,74}-zip php{73,74}-pecl-apc php{73,74}-mysql

# All good, apart from PHP is not running...

# RUN su -c "setenforce 0"

RUN mkdir /var/www/vhosts
RUN chmod 777 /var/www/vhosts

COPY ./httpd.conf /etc/httpd/conf/httpd.conf
COPY ./ssl.conf /etc/httpd/conf.d/ssl.conf
COPY ./vhosts.conf /etc/httpd/conf.d/virtual.conf

# Certificate files
RUN mkdir /etc/httpd/conf.d/ssl
COPY ./certs/*.crt /etc/httpd/conf.d/ssl
COPY ./certs/*.key /etc/httpd/conf.d/ssl

ADD ./php.php /var/www/html/php.php

EXPOSE 80
EXPOSE 443
EXPOSE 3306

COPY ./startup.sh /usr/local/bin/startup.sh
RUN chmod +x /usr/local/bin/startup.sh

CMD ["/usr/local/bin/startup.sh"]