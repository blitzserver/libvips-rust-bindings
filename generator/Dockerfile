# (c) Copyright 2019-2020 OLX
FROM rust:1.45-alpine3.12

ENV VIPS_VERSION=8.11.4

RUN apk add --update --no-cache --repository=http://dl-cdn.alpinelinux.org/alpine/edge/community \
            build-base \
            imagemagick \
            imagemagick-dev \
            gtk-doc \
            imagemagick-libs \
            autoconf \
            automake \
            pkgconfig \
            openssl-dev\
            clang \
            glib-dev \
            expat-dev \
            tiff-dev \
            libjpeg-turbo-dev \
            libexif-dev \
            giflib-dev \
            librsvg-dev \
            lcms2-dev \
            libpng-dev \
            orc-dev \
            libwebp-dev \
            libimagequant-dev \
            gobject-introspection-dev \
            fftw-dev \
            pango-dev \
            libgsf-dev 

RUN wget https://github.com/blitzserver/libvips/archive/refs/heads/master.tar.gz

RUN mkdir vips

RUN tar xvzf master.tar.gz -C vips --strip-components 1

WORKDIR /vips

RUN ./autogen.sh --enable-debug=yes --without-python

RUN ./configure --enable-debug=yes --without-python

RUN make

RUN make install

RUN ldconfig /etc/ld.so.conf.d

WORKDIR /

RUN rm -rf vips

RUN rm -f master.tar.gz

RUN rustup component add rustfmt --toolchain 1.45.2-x86_64-unknown-linux-musl
