FROM php:8.2-cli

# install base packages
RUN apt-get update --fix-missing && \
    apt-get install -y --no-install-recommends apt-utils \
    unzip \
    procps \
    cron \
    libsox-fmt-mp3 \
    sox \
    ffmpeg

RUN docker-php-ext-install mysqli pdo pdo_mysql calendar && docker-php-ext-enable pdo_mysql

WORKDIR /var/www/app

# Create the log file to be able to run tail
RUN touch /var/log/cron.log

# Setup cron job
RUN (crontab -l ; echo "* * * * * cd /var/www/app/ && /usr/local/bin/php artisan schedule:run >> /var/log/cron.log") | crontab

# Run the command on container startup
CMD cron && echo "cron started" && tail -f /var/log/cron.log
