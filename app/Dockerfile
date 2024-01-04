FROM cthulhoo/ttrss-fpm-pgsql-static:latest

RUN apk add php83-ldap

# Healthcheck
RUN apk add fcgi &&\
    wget -O /usr/local/bin/php-fpm-healthcheck https://raw.githubusercontent.com/renatomefi/php-fpm-healthcheck/master/php-fpm-healthcheck &&\
    chmod +x /usr/local/bin/php-fpm-healthcheck
HEALTHCHECK --interval=10s CMD php-fpm-healthcheck

# Plugins
WORKDIR /var/www/html/tt-rss/plugins.local
RUN git clone https://github.com/pasbec/ttrss-auth-ldap.git auth_ldap
RUN git clone https://git.tt-rss.org/fox/ttrss-mailer-smtp.git/ mailer_smtp

WORKDIR /opt/tt-rss