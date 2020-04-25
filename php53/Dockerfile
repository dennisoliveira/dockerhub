FROM ubuntu:12.04

ARG USER=ubuntu

# Update repositories
RUN apt-get update && apt-get upgrade

# Install sudo and add default user
RUN apt-get update && apt-get -y install sudo
RUN adduser --disabled-password --gecos '' $USER
RUN adduser $USER sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Install Helpers
RUN apt-get install vim -y

# Install Apache
RUN apt-get install apache2 -y
RUN a2enmod rewrite

# Install PHP 5.3
RUN apt-get install -y php5 \
  php5-common \
  php5-cli \
  php5-dev \
  php5-mysql \
  php5-pgsql \
  php5-gd \
  php5-mcrypt \
  php5-curl \
  php-pear \
  libapache2-mod-php5 \
  php5-xdebug

USER $USER
WORKDIR /home/$USER

# ENTRYPOINT
EXPOSE 80
CMD ["sudo","/usr/sbin/apache2ctl", "-D", "FOREGROUND"]