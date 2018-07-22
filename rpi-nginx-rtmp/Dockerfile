FROM resin/rpi-raspbian:stretch

#RUN [ "cross-build-start" ]

# Install dependencies
RUN apt-get update \
	&& apt-get install build-essential wget unzip libpcre3 libpcre3-dev libssl-dev

# Download nginx with rtmp module
RUN wget http://nginx.org/download/nginx-1.13.1.tar.gz \
	&& wget https://github.com/arut/nginx-rtmp-module/archive/master.zip \
	&& tar -zxvf nginx-1.13.1.tar.gz \
	&& unzip master.zip

# Compile nginx
RUN cd nginx-1.13.1 \
	&& ./configure --without-http_gzip_module --with-http_ssl_module  --add-module=../nginx-rtmp-module-master \
	&& make \
	&& make install

# Configure
ADD nginx.conf ./nginx-rtmp.conf
RUN cat nginx-rtmp.conf >> /usr/local/nginx/conf/nginx.conf

# Start nginx
CMD /usr/local/nginx/sbin/nginx -g "daemon off;"

EXPOSE 1935


