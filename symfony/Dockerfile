FROM composer/composer:latest

MAINTAINER Diyloc <technical@diyloc.com>

# Install New Relic
RUN apt-get update
RUN apt-get -y install wget
RUN apt-get -y install python-setuptools

RUN easy_install pip
RUN mkdir -p /opt/newrelic
WORKDIR /opt/newrelic

RUN wget -r -nd --no-parent -Alinux.tar.gz \
    http://download.newrelic.com/php_agent/release/ >/dev/null 2>&1 \
    && tar -xzf newrelic-php*.tar.gz --strip=1

ENV NR_INSTALL_SILENT true
RUN export NR_INSTALL_KEY=NEW_RELIC_LICENSE_KEY
RUN bash newrelic-install install
RUN pip install newrelic-plugin-agent

RUN mkdir -p /var/log/newrelic
RUN mkdir -p /var/run/newrelic

# Install NodeJs
RUN curl -sL https://deb.nodesource.com/setup_4.x | bash -
RUN apt-get install -y nodejs git && \
    npm install gulp-cli bower -g

ARG PUID=1000
ARG PGID=1000
RUN groupadd -g $PGID symfony && \
    useradd -u $PUID -g symfony -m symfony

RUN mkdir -p /var/www/symfony

WORKDIR /var/www/symfony
COPY . /var/www/symfony

RUN chown -R symfony:symfony /var/www/symfony
RUN chmod 755 /var/www/symfony/var -R

USER symfony

RUN composer install --no-ansi --no-dev --no-interaction --no-progress --no-scripts --optimize-autoloader

VOLUME /var/www/symfony
