FROM ubuntu
MAINTAINER Karol Majta <karol[at]lambdafizz.com>

RUN apt-get update
RUN apt-get install -y wget build-essential libpcre3 libpcre3-dev zlib1g zlib1g-dev
RUN wget --no-check-certificate https://github.com/nginx/nginx/archive/v1.4.7.tar.gz
RUN tar -xf v1.4.7.tar.gz
RUN rm v1.4.7.tar.gz
RUN cd nginx-1.4.7 && ./configure && make && make install
RUN rm -r nginx-1.4.7
RUN mkdir /usr/local/nginx/conf/sites-enabled

ADD files/nginx.conf /usr/local/nginx/conf/nginx.conf

VOLUME ["/usr/local/nginx/conf/sites-enabled"]
EXPOSE 80

CMD /usr/local/nginx/sbin/nginx
