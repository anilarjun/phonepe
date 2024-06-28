FROM php:8.3-fpm

RUN apt-get update -y && apt-get install -y \
    libmcrypt-dev unzip zip git supervisor cron \
    && docker-php-ext-install mysqli pdo pdo_mysql bcmath

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

COPY image/supervisor/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
ADD cron/crontab /etc/cron.d/cron
RUN chmod 0644 /etc/cron.d/cron && touch /var/log/crontab.log

CMD ["/usr/bin/supervisord", "-n", "-c", "/etc/supervisor/conf.d/supervisord.conf"]

WORKDIR /var/www/html
