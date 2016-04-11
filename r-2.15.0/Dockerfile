FROM docker.io/ubuntu:14.04

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

RUN curl -O http://cran.stat.ucla.edu/src/base/R-2/R-2.15.0.tar.gz \
        && tar xvf R-2.15.0.tar.gz \
        && cd R-2.15.0 \
        && ./configure --with-recommended-packages \
        && make \
        && make install \
        && cd /usr/local/bin \
        && mv R R2150 \
        && mv Rscript Rscript2150 \
        && ln -s R2150 R2 \
        && ln -s Rscript2150 R2script

CMD ["R2"]
