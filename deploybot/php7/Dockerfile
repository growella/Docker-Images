from php:7.0.13-cli

RUN cd /tmp && \
	/usr/bin/curl -sL -o setup_6.x https://deb.nodesource.com/setup_6.x && \
	bash setup_6.x && \
	/usr/bin/apt-get install -y nodejs git zlib1g-dev && \
	npm -g install yarn gulp && \
	docker-php-ext-install zip

# Register the COMPOSER_HOME environment variable
ENV COMPOSER_HOME /composer

# Add global binary directory to PATH and make sure to re-export it
ENV PATH /composer/vendor/bin:$PATH

# Allow Composer to be run as root
ENV COMPOSER_ALLOW_SUPERUSER 1

# Setup the Composer installer
RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer \
  && curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig \
  && php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { unlink('/tmp/composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }"

ENV COMPOSER_VERSION 1.2.0
# Install Composer
RUN php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer --version=${COMPOSER_VERSION} && rm -rf /tmp/composer-setup.php
