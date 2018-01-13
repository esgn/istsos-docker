FROM alpine:3.4

ENV APACHE_LOG_DIR /var/log/apache2

# Install dependencies
RUN (apk update && apk add apache2 apache2-mod-wsgi py-psycopg2 py-dateutil)

# Extract istsos
COPY files/istsos-2.3.1.tar.gz /tmp
RUN (tar -zxvf /tmp/istsos-2.3.1.tar.gz -C /usr/local/)
RUN (chmod 755 -R /usr/local/istsos && chown -R apache:apache /usr/local/istsos/services && chown -R apache:apache /usr/local/istsos/logs)

# Replace apache default conf
RUN (mkdir /etc/apache2/vhost.d && echo "IncludeOptional /etc/apache2/vhost.d/*.conf" >> /etc/apache2/httpd.conf)
COPY files/000-default.conf /etc/apache2/vhost.d

# Expose HTTP port
EXPOSE 80

# Default command for docker run
RUN (mkdir /run/apache2)
RUN (mkdir /var/www/html)
# Output to console for debug purposes
# RUN (sed -ri -e 's!^(\s*CustomLog)\s+\S+!\1 /proc/self/fd/1!g' -e 's!^(\s*ErrorLog)\s+\S+!\1 /proc/self/fd/2!g' "/etc/apache2/httpd.conf")
CMD ["httpd","-D","FOREGROUND"]
