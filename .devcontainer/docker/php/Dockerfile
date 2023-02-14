FROM skilldlabs/php:81

ARG BUILD_DATE
ARG VCS_REF

LABEL org.label-schema.build-date=$BUILD_DATE \
  org.label-schema.vcs-ref=$VCS_REF \
  org.label-schema.schema-version="1.0" \
  org.label-schema.name="docker-php" \
  org.label-schema.description="PHP-FPM 8 Alpinelinux for Drupal - git, composer, drush 8, sqlite, patch" \
  org.label-schema.vcs-url="https://github.com/skilld-labs/docker-php" \
  maintainer="Andy Postnikov <andypost@ya.ru>, Oleksiy Stepaniuk <ostepaniuk@skilld.cloud>"

RUN apk add --no-cache \
  php8-pecl-memcached \
  php8-pecl-imagick \
  php8-soap \
  git \
  shadow


RUN set -e \
  && mkdir -p /workspace \
  && (delgroup www-data || true) \
  && addgroup -g 1000 -S www-data \
  && adduser -u 1000 -D -S -G www-data www-data \
  && apk add --no-cache \
  php8-fpm

COPY php-fpm.conf /etc/php8/

#USER www-data
WORKDIR /workspace
VOLUME /workspace

EXPOSE 9000

CMD ["php-fpm8", "-F"]
