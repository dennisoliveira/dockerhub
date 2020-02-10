FROM ubuntu:16.04

# Update repositories and update system
RUN apt-get update -y && apt-get upgrade -y

# Install language-pack and add repository
RUN apt-get install -y software-properties-common vim
RUN apt-get install -y language-pack-en-base
RUN LC_ALL=en_US.UTF-8 add-apt-repository -y ppa:ondrej/php && apt-get update -y

# Install Apache
RUN apt-get install apache2 -y
RUN a2enmod rewrite

RUN apt-get update -y && apt-get install -y php7.1 \
  php7.1-mbstring \
  php7.1-curl \
  php7.1-xmlrpc \
  php7.1-soap \
  php7.1-zip \
  php7.1-gd \
  php7.1-simplexml \
  php7.1-intl \
  php7.1-mysql \
  php7.1-sqlite3 \
  php7.1-uploadprogress \
  php-pear

RUN apt-get clean

RUN update-alternatives --set php /usr/bin/php7.1
RUN a2dismod php7.3
RUN a2enmod php7.1
RUN service apache2 restart

# ENTRYPOINT
EXPOSE 80
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]