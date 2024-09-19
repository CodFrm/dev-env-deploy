FROM node:18-alpine3.18 AS build

ARG ARIANG_VERSION=1.3.7 \
	ARIA2_VERSION=1.37.0

RUN apk update && apk add tzdata &&  \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime &&  \
    echo "Asia/Shanghai" > /etc/timezone

WORKDIR /aria

RUN apk add git && \
	git clone https://github.com/mayswind/AriaNg.git

RUN cd AriaNg && \
	git checkout tags/${ARIANG_VERSION} && \
	npm install && \
	npm run build

RUN cd ../ && \
	git clone https://github.com/aria2/aria2.git

RUN apk add gcc g++ make autoconf automake gettext-dev libxml2-dev cppunit-dev libtool gnutls-dev \
	nettle-dev gmp-dev libssh2-dev c-ares-dev zlib-dev sqlite-dev

RUN cd aria2 && \
	git checkout tags/release-${ARIA2_VERSION} && \
	autoreconf -i && \
	./configure ARIA2_STATIC=yes && \
	make

FROM nginx:1.25-alpine3.18

# ariaNg

RUN apk add nginx

COPY --from=build /aria/AriaNg/dist /usr/share/nginx/html


# aria2
