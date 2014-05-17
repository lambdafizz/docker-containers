FROM cmfatih/golang
MAINTAINER Karol Majta <karol[at]lambdafizz.com>

RUN apt-get update
RUN apt-get install -y wget
RUN wget http://skydb.io/sky-0.3.0.tar.gz
RUN tar -xvf sky-0.3.0.tar.gz
WORKDIR /go/sky-0.3.0
RUN make deps
RUN go get github.com/gorilla/mux
RUN go get github.com/jmhodges/levigo
RUN go get github.com/ugorji/go-msgpack
RUN make
RUN make install
RUN ldconfig
RUN chmod +x /go/sky-0.3.0/build/skyd
VOLUME ["/var/lib/sky"]
EXPOSE 8585
CMD ["/go/sky-0.3.0/build/skyd"]
