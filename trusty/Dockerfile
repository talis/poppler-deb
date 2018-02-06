FROM ubuntu:14.04

RUN apt-get update; \
    apt-get upgrade -y; \
    apt-get install -y --force-yes build-essential ruby1.9 gettext \
        libopenjpeg-dev libopenjpeg2 curl xz-utils gcc make g++ \
        libjpeg-dev pkg-config fontconfig autoconf libfontconfig1-dev \
        libjpeg-dev libopenjpeg-dev libglib2.0-dev gtk-doc-tools \
        libyelp-dev yelp-tools gobject-introspection libsecret-1-dev \
        libnautilus-extension-dev; gem install fpm
RUN cd ~; \
    curl -s https://poppler.freedesktop.org/poppler-0.59.0.tar.xz | tar xJ
RUN mkdir /out; \
    mkdir /tmp/out; \
    cd ~/poppler-0.59.0; \
    LIBOPENJPEG_LIBS=/usr/lib/x86_64-linux-gnu ./configure; \
    make; \
    make install DESTDIR=/tmp/out
CMD fpm -s dir -t deb -n poppler -v 0.59.0.1-trusty -C /tmp/out \
        -p poppler_VERSION_ARCH.deb \
        -d "libopenjpeg-dev (>=0)" \
        -d "libopenjpeg2 (>=0)" \
        -d "libjpeg-dev (>=0)" \
        -d "fontconfig (>=0)" \
        -d "libfontconfig1-dev (>=0)" \
        -d "libjpeg-dev (>=0)" \
        -d "libopenjpeg-dev (>=0)" \
        -d "libglib2.0-dev (>=0)" \
        --deb-shlibs \
        usr/local; \
    cp *.deb /out
