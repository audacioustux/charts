FROM docker.io/bitnami/moodle:4.5.2-debian-12-r4

USER root

# enable redis
RUN install_packages php-redis

RUN set -ex \
    && mkdir /tmp/localcachedir \
    && apt update && apt -y install autoconf build-essential \
    && rm -rvf /var/lib/apt/lists*... \
    && pecl channel-update pecl.php.net \
    && pecl install -o igbinary \
    && pecl install -o -D 'enable-redis-igbinary="yes"' redis \
    && echo "extension=redis.so" >> /opt/bitnami/php/lib/php.ini \
    && echo "extension=igbinary.so" >> /opt/bitnami/php/lib/php.ini \
    && rm -rvf /tmp/pear

# enable cron
RUN echo "0 * * * * daemon /opt/bitnami/php/bin/php /opt/bitnami/moodle/admin/cli/cron.php 2>&1 > /dev/null" > /etc/cron.d/moodle-cron
RUN echo "* * * * * daemon /opt/bitnami/php/bin/php /opt/bitnami/moodle/admin/cli/adhoc_task.php --execute --keep-alive=59 2>&1 > /dev/null" >> /etc/cron.d/moodle-cron

USER 1001