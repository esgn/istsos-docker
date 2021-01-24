# For testing purposes with new alpine version
# run it in interactive mode
# docker run -it --rm --name alpine alpine:3.13
FROM alpine:3.13

ENV APACHE_LOG_DIR /var/log/apache2
ARG ISTSOS_VERSION=2.4.0-RC4

# Install dependencies
RUN (apk update && apk add apache2 apache2-mod-wsgi py3-psycopg2 py3-dateutil py3-pip postgresql-dev python3-dev gcc musl-dev libxml2-dev libxslt-dev)

# Extract istsos
COPY files/istsos-$ISTSOS_VERSION.tar.gz /tmp
RUN (tar -zxf /tmp/istsos-$ISTSOS_VERSION.tar.gz -C /usr/local/)
RUN (chmod 755 -R /usr/local/istsos && chown -R apache:apache /usr/local/istsos/services && chown -R apache:apache /usr/local/istsos/logs)

# Install pip3 requirements
RUN pip3 install -r /usr/local/istsos/requirements.txt

# Copy test datasets
COPY files/dataset /tmp/dataset
COPY files/tutorial /tmp/tutorial

# Replace apache default conf
RUN (mkdir /etc/apache2/vhost.d && echo "IncludeOptional /etc/apache2/vhost.d/*.conf" >> /etc/apache2/httpd.conf)
COPY files/000-default.conf /etc/apache2/vhost.d

# Expose HTTP port
EXPOSE 80

# Create necessary files
# RUN (mkdir /run/apache2) => Not useful anymore ?
RUN (mkdir /var/www/html)

# Output istsos logs to console for debug purposes
# RUN (sed -ri -e 's!^(\s*CustomLog)\s+\S+!\1 /proc/self/fd/1!g' -e 's!^(\s*ErrorLog)\s+\S+!\1 /proc/self/fd/2!g' "/etc/apache2/httpd.conf")

CMD ["httpd","-D","FOREGROUND"]
