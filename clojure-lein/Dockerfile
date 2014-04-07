FROM dockerfile/java
MAINTAINER Karol Majta <karol[at]lambdafizz.com>

RUN apt-get update
RUN apt-get install -y wget maven
RUN wget --no-check-certificate -O /bin/lein https://raw.github.com/technomancy/leiningen/stable/bin/lein
RUN chmod a+x /bin/lein
ENV LEIN_ROOT true
# we need to add maven local cache as volume, so deps don't get
# fetched on every run in container
VOLUME ["/root/.m2"]
# request lein version to prefetch it and then commit
RUN lein version
