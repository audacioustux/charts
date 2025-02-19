FROM docker.io/bitnami/moodle:4.5.2-debian-12-r0

USER root

# enable redis
RUN install_packages php-redis vim

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

USER 1001