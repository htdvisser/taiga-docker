FROM debian:wheezy

MAINTAINER Hylke Visser <htdvisser@gmail.com>

# Install NginX
RUN apt-key adv --keyserver pgp.mit.edu --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62
RUN echo "deb http://nginx.org/packages/mainline/debian/ wheezy nginx" >> /etc/apt/sources.list

ENV NGINX_VERSION 1.7.10-1~wheezy

RUN apt-get update && apt-get install -y git nginx=${NGINX_VERSION} && rm -rf /var/lib/apt/lists/*

# NginX Configuration
ADD nginx.conf /etc/nginx/nginx.conf
ADD mime.types /etc/nginx/mime.types
ADD web.conf /etc/nginx/web.conf

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

# Install taiga-front-dist
RUN \
  mkdir -p /usr/local/taiga && \
  git clone https://github.com/taigaio/taiga-front-dist.git /usr/local/taiga/taiga-front-dist && \
  cd /usr/local/taiga/taiga-front-dist && \
  git checkout stable

# Configuration and Start scripts
ADD ./configure /usr/local/taiga/configure
ADD ./start /usr/local/taiga/start
RUN chmod +x /usr/local/taiga/configure /usr/local/taiga/start

EXPOSE 80

CMD ["/usr/local/taiga/start"]
