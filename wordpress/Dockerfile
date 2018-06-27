ARG FROM_PREFIX

FROM ${FROM_PREFIX}python3

WORKDIR /root

RUN    apt-get update \
    && apt-get install --no-install-recommends -y \
                       wget unzip wordpress php-sqlite3 \
    && rm -rf /var/lib/apt/lists/* \
    && a2dissite 000-default

RUN    wget https://downloads.wordpress.org/plugin/sqlite-integration.1.8.1.zip \
    && unzip sqlite-integration.*.zip -d /var/lib/wordpress/wp-content/plugins/ \
    && chown -R www-data /var/lib/wordpress/wp-content/plugins/sqlite-integration \
    && cp /var/lib/wordpress/wp-content/plugins/sqlite-integration/db.php /var/lib/wordpress/wp-content/ \
    && rm sqlite-integration.*.zip

RUN    wget https://downloads.wordpress.org/plugin/indieweb.3.3.8.zip \
    && unzip indieweb.*.zip -d /var/lib/wordpress/wp-content/plugins/ \
    && rm indieweb.*.zip

RUN    wget https://raw.github.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
    && true

RUN    wget https://downloads.wordpress.org/theme/independent-publisher.1.8.zip \
    && unzip independent-publisher.*.zip -d /var/lib/wordpress/wp-content/themes/ \
    && rm independent-publisher.*.zip

COPY wp.conf /etc/apache2/sites-available/
COPY config-default.php /etc/wordpress/

RUN    a2ensite wp

EXPOSE 443/tcp
EXPOSE 80/tcp

CMD [ "apache2ctl", "-X" ]
