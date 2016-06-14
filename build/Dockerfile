# alpine linux with swagger-editor
FROM youske/alpine-nodejs:latest
MAINTAINER youske miyakoshi <youske@gmail.com>

ENV PORT=8081 \
    WORKER_CONNECTION=512 \
    CHARSET=ja_JP.UTF-8

ENV PACKAGE='nginx git ' \
    BUILDPACKAGE="build-base musl-dev nodejs-dev python-dev linux-headers"

WORKDIR /
USER root

# swagger-ui dependencies package install
RUN apk add ${PACKAGE} --no-cache && apk add ${BUILDPACKAGE} --no-cache -t buildpackage

RUN git clone https://github.com/swagger-api/swagger-editor.git && \
    cd swagger-editor && \
    npm install && npm run build

RUN apk del buildpackage --no-cache && rm -rf /tmp/* /var/cache/apk/*

EXPOSE ${PORT}

WORKDIR /swagger-editor
ENTRYPOINT ["switch","shell=/bin/bash","--","npm","start"]
