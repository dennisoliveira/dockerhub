FROM php:5.6-apache

ARG USER=ubuntu

# Update repositories and update system
RUN apt-get update -y \
  && apt-get -y install sudo

RUN adduser --disabled-password --gecos '' $USER
RUN adduser $USER sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

RUN apt-get update && apt-get install -y \
  libmcrypt-dev \
  && docker-php-ext-install -j$(nproc) mcrypt mbstring

RUN pecl install uploadprogress

# ENTRYPOINT
EXPOSE 80
CMD ["sudo","/usr/sbin/apache2ctl", "-D", "FOREGROUND"]