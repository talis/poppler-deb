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
CMD fpm -s dir -t deb -n poppler -v 0.59.0-trusty -C /tmp/out \
        -p poppler_VERSION_ARCH.deb \
        -d "ld-linux-x86-64.so.2  (>=0)" \
        -d "libX11.so.6  (>=0)" \
        -d "libXau.so.6  (>=0)" \
        -d "libXdmcp.so.6  (>=0)" \
        -d "libXext.so.6  (>=0)" \
        -d "libXrender.so.1  (>=0)" \
        -d "libc.so.6  (>=0)" \
        -d "libcairo.so.2  (>=0)" \
        -d "libdl.so.2  (>=0)" \
        -d "libexpat.so.1  (>=0)" \
        -d "libfontconfig.so.1  (>=0)" \
        -d "libfreetype.so.6  (>=0)" \
        -d "libgcc_s.so.1  (>=0)" \
        -d "libm.so.6  (>=0)" \
        -d "libpixman-1.so.0  (>=0)" \
        -d "libpng12.so.0  (>=0)" \
        -d "libpoppler.so.70  (>=0)" \
        -d "libpthread.so.0  (>=0)" \
        -d "librt.so.1  (>=0)" \
        -d "libstdc++.so.6  (>=0)" \
        -d "libxcb-render.so.0  (>=0)" \
        -d "libxcb-shm.so.0  (>=0)" \
        -d "libxcb.so.1  (>=0)" \
        -d "libz.so.1  (>=0)" \
        -d "linux-vdso.so.1  (>=0)" \
        --deb-shlibs \
        usr/local; \
    cp *.deb /out
