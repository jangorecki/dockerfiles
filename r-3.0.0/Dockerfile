FROM docker.io/ubuntu:16.04

MAINTAINER Jan Gorecki j.gorecki@wit.edu.pl

RUN apt-get update -qq \
        && apt-get upgrade -y

RUN apt-get install -y --no-install-recommends \
                apt-transport-https \
                software-properties-common \
                curl \
                git \
                libssl-dev \
                libcurl4-gnutls-dev \
                vim \
        && rm -rf /var/lib/apt/lists/*

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt-get update -qq \
        && apt-get -y --no-install-recommends \
                build-dep \
                r-base-dev \
        && rm -rf /var/lib/apt/lists/*

RUN curl -O http://cran.stat.ucla.edu/src/base/R-3/R-3.0.0.tar.gz \
        && tar xvf R-3.0.0.tar.gz \
        && cd R-3.0.0/ \
        && ./configure --with-recommended-packages \
        && make \
        && make install \
        && cd /usr/local/bin \
        && mv R R300 \
        && mv Rscript Rscript300 \
        && ln -s R300 R3 \
        && ln -s Rscript300 R3script

CMD ["R3"]
