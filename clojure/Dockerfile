FROM alpine:latest

MAINTAINER qinains <qinains@qq.com>

ENV PATH $PATH:/usr/lib/jvm/default-jvm/bin
ENV LEIN_ROOT true

RUN apk --no-cache add openjdk8 ttf-dejavu bash

RUN wget -q -O /usr/bin/lein https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein \
&& chmod +x /usr/bin/lein \
&& lein

CMD ["bash"]
