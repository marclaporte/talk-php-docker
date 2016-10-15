FROM ubuntu:16.04

# install main pachages and enable vhosts
RUN apt-get update \
	&& apt-get install -y apache2 tinyproxy dnsmasq supervisor \
	&& a2enmod vhost_alias \
	&& a2enmod proxy \
    && a2enmod proxy_fcgi \
	&& a2dissite 000-default \
	&& ln -s ../sites-available/000-vhosts.conf /etc/apache2/sites-enabled/000-vhosts.conf \
	&& sed -i 's,^ErrorLog .*,ErrorLog /dev/stderr,' /etc/apache2/apache2.conf \
	&& mkdir /var/lock/apache2 && chown www-data /var/lock/apache2 \
	&& mkdir /var/run/apache2 \
	&& sed -i 's,#Allow 192.168.0.0/16,Allow 192.168.0.0/16,' /etc/tinyproxy.conf \
	&& sed -i 's,#Allow 172.16.0.0/12,Allow 172.16.0.0/12,' /etc/tinyproxy.conf \
	&& sed -i 's,#Allow 10.0.0.0/8,Allow 10.0.0.0/8,' /etc/tinyproxy.conf \
	&& mkdir /var/run/tinyproxy && chown nobody /var/run/tinyproxy && chgrp nogroup /var/run/tinyproxy

# Add other config files
ADD vhosts.conf /etc/apache2/sites-available/000-vhosts.conf
ADD dnsmasq.conf /etc/dnsmasq.conf
ADD resolv.dnsmasq.conf /etc/resolv.dnsmasq.conf
ADD supervisor.conf /etc/supervisor/conf.d/php-docker.conf
ADD fix_resolv.sh /fix_resolv.sh

VOLUME /var/www/html
EXPOSE 80
EXPOSE 8888

#ENTRYPOINT ["httpd","-DFOREGROUND" ]
#ENTRYPOINT ["supervisord"]
