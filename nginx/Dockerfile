FROM ubuntu
MAINTAINER Karol Majta <karol[at]lambdafizz.com>

RUN apt-get update
RUN apt-get install -y wget build-essential libpcre3 libpcre3-dev zlib1g zlib1g-dev lua5.1 liblua5.1-dev
RUN wget --no-check-certificate -O nginx_devel_kit-0.2.19.tar.gz https://github.com/simpl/ngx_devel_kit/archive/v0.2.19.tar.gz
RUN wget --no-check-certificate -O lua-nginx-module-0.9.6.tar.gz https://github.com/chaoslawful/lua-nginx-module/archive/v0.9.6.tar.gz
RUN wget --no-check-certificate -O nginx-1.4.7.tar.gz https://github.com/nginx/nginx/archive/v1.4.7.tar.gz
RUN tar -xf nginx_devel_kit-0.2.19.tar.gz
RUN tar -xf lua-nginx-module-0.9.6.tar.gz
RUN tar -xf nginx-1.4.7.tar.gz
RUN rm nginx_devel_kit-0.2.19.tar.gz lua-nginx-module-0.9.6.tar.gz nginx-1.4.7.tar.gz
RUN cd nginx-1.4.7 && ./configure --add-module=/ngx_devel_kit-0.2.19 --add-module=/lua-nginx-module-0.9.6 && make && make install
RUN rm -r ngx_devel_kit-0.2.19 lua-nginx-module-0.9.6 nginx-1.4.7
RUN mkdir /usr/local/nginx/conf/sites-enabled
RUN mkdir /usr/local/nginx/conf.d

ADD files/nginx.conf /usr/local/nginx/conf/nginx.conf

VOLUME ["/usr/local/nginx/conf/sites-enabled", "/usr/local/nginx/conf/conf.d"]
EXPOSE 80

CMD /usr/local/nginx/sbin/nginx
