FROM ubuntu:16.04

MAINTAINER Jan Gorecki j.gorecki@wit.edu.pl

RUN apt-get update -qq \
        && apt-get upgrade -y

RUN apt-get install -y --no-install-recommends \
                apt-transport-https \
                software-properties-common \
                curl \
                wget \
                git \
                libssl-dev \
                libcurl4-gnutls-dev \
                vim \
                locales \
                dbus \
                qpdf \
        && rm -rf /var/lib/apt/lists/*

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# R 3.5 changed url, revert when 3.6 released
RUN add-apt-repository -s "deb https://cloud.r-project.org/bin/linux/ubuntu $(lsb_release -cs)-cran35/" \
        && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9

RUN apt-get update -qq \
        && apt-get -y --no-install-recommends \
                build-dep \
                r-base-dev \
        && rm -rf /var/lib/apt/lists/*

RUN curl -O https://stat.ethz.ch/R/daily/R-devel.tar.gz \
        && tar xvf R-devel.tar.gz \
        && cd R-devel/ \
        && ./configure --with-recommended-packages --enable-strict-barrier --disable-long-double \
        && make \
        && make install

RUN echo 'options(repos = c(CRAN = "https://cloud.r-project.org"), download.file.method = "libcurl")' >> /usr/local/lib/R/etc/Rprofile.site \
        && mkdir -p ~/.R \
        && echo 'CFLAGS=-g -O2 -Wall -pedantic -fstack-protector-strong -D_FORTIFY_SOURCE=2' > ~/.R/Makevars \
        && echo 'CXXFLAGS=-g -O2 -Wall -pedantic -fstack-protector-strong -D_FORTIFY_SOURCE=2' >> ~/.R/Makevars

CMD ["R"]
