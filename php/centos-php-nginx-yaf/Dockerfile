FROM centos:7
MAINTAINER lfq618@gmail.com
RUN rpm -Uvh http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
	&& rpm -Uvh https://sp.repo.webtatic.com/yum/el7/webtatic-release.rpm \
	&& yum update -y \
	&& yum install -y wget \
		sed \ 
		gcc \
		gcc-c++ \
		gd \
		gd-devel \
		gmp-devel \
		epel-release \
		net-tools \
		ntpdate \
		ntp \
		openssh-clients \ 
		curl \
		crontabs \
		openssl \
		openssl-devel \
		nginx \
		squid \
		php71w \
		php71w-fpm \
		php71w-gd \
		php71w-soap \
		php71w-pdo_mysql \
		php71w-pear \
		php71w-devel \	
		php71w-mbstring \
		php71w-mcrypt \
		php71w-ldap \
	&& yum update -y ntp ntpdate kernel-headers \
	&& yum clean all \
	&& sed -i 's/http_access deny all/#http_access deny all/g' /etc/squid/squid.conf \
	&& cd /tmp \
	&& wget -O get-pip.py https://bootstrap.pypa.io/get-pip.py \
	&& python get-pip.py \
	&& pip install supervisor \
	&& pecl install yaf \
	&& pecl install redis \
	&& echo "" >> /etc/php.ini \
	&& echo "extension=redis.so" >> /etc/php.ini \
	&& echo "extension=yaf.so" >> /etc/php.ini \
	&& echo "[yaf]" >> /etc/php.ini \
 	&& echo "yaf.use_namespace = 1" >> /etc/php.ini 

RUN echo "<?php echo phpinfo();" >> /var/www/html/public/index.php
COPY resources/etc/ /etc/
EXPOSE 80 443
WORKDIR /var/www/html
CMD ["supervisord","-c","/etc/supervisor/supervisord.conf"]
