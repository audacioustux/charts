FROM docker.io/bitnami/moodle:4.5.2-debian-12-r4

USER root

# enable redis
RUN install_packages php-redis vim cron autoconf build-essential

RUN set -ex \
    && pecl channel-update pecl.php.net \
    && pecl install -o igbinary \
    && pecl install -o -D 'enable-redis-igbinary="yes"' redis \
    && echo "extension=redis.so" >> /opt/bitnami/php/lib/php.ini \
    && echo "extension=igbinary.so" >> /opt/bitnami/php/lib/php.ini

# enable cron
RUN echo "* * * * * daemon /opt/bitnami/php/bin/php /opt/bitnami/moodle/admin/cli/cron.php" | crontab -u daemon -

USER 1001