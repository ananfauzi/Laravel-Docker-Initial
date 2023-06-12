# Use php:8.1-apache image
FROM php:8.1-apache

# Enable apache mod_rewrite
RUN a2enmod rewrite

# Install dependency
RUN apt update \
	&& apt install -y \
		g++ \
		libicu-dev \
		libpq-dev \
		libzip-dev \
		zip \
		zlib1g-dev \
	&& docker-php-ext-install \
		intl \
		opcache \
		pdo \
		pdo_mysql

# Setup working directory
WORKDIR /var/www/laravel

# Do not use root as user, create new user
RUN /usr/sbin/useradd --create-home --home-dir /usr/local/anan --shell /bin/bash anan
RUN /usr/sbin/adduser anan sudo

# Add permission
RUN chown -R anan /usr/local/
RUN chown -R anan /usr/lib/
RUN chown -R anan /usr/bin/
RUN chown -R anan /var/www/laravel

# Use new user
USER anan

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install node, npm
ENV NODE_VERSION=16.13.0
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
ENV NVM_DIR=/usr/local/anan/.nvm
RUN . "$NVM_DIR/nvm.sh" && nvm install ${NODE_VERSION}
RUN . "$NVM_DIR/nvm.sh" && nvm use v${NODE_VERSION}
RUN . "$NVM_DIR/nvm.sh" && nvm alias default v${NODE_VERSION}
ENV PATH="/usr/local/anan/.nvm/versions/node/v${NODE_VERSION}/bin/:${PATH}"
