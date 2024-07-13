FROM php:8.2-cli

# install additional software
RUN apt-get update --fix-missing && \
    apt-get install -y procps


RUN apt-get install -y git make cmake gcc g++ libmad0-dev redis-tools redis-server \
  libid3tag0-dev libsndfile1-dev libgd-dev libboost-filesystem-dev \
  libboost-program-options-dev \
  libboost-regex-dev

RUN docker-php-ext-install mysqli pdo pdo_mysql calendar && docker-php-ext-enable pdo_mysql

WORKDIR /var/www/app
ENTRYPOINT [ "php", "artisan" ]
CMD ["queue:work"]
