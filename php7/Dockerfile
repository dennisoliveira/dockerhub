FROM ubuntu:16.04

# Update repositories and update system
RUN apt-get update -y && apt-get upgrade -y

# Install sudo and add default user
RUN apt-get update && apt-get -y install sudo
RUN adduser --disabled-password --gecos '' $USER
RUN adduser $USER sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Install language-pack and add repository
RUN apt-get install -y software-properties-common vim curl zip unzip
RUN apt-get install -y language-pack-en-base
RUN LC_ALL=en_US.UTF-8 add-apt-repository -y ppa:ondrej/php && apt-get update -y

# Install Apache
RUN apt-get install apache2 -y
RUN a2enmod rewrite

RUN apt-get update -y && apt-get install -y php7.2 \
  php7.2-mbstring \
  php7.2-curl \
  php7.2-xmlrpc \
  php7.2-soap \
  php7.2-zip \
  php7.2-gd \
  php7.2-simplexml \
  php7.2-intl \
  php7.2-mysql \
  php7.2-sqlite3 \
  php7.2-uploadprogress \
  php-pear

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

USER $USER
WORKDIR /home/$USER

# ENTRYPOINT
EXPOSE 80
CMD ["sudo", "/usr/sbin/apache2ctl", "-D", "FOREGROUND"]