FROM ubuntu:16.04

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

RUN curl -O https://cloud.r-project.org/src/base/R-devel/R-devel.tar.gz \
        && tar xvf R-devel.tar.gz \
        && cd R-devel/ \
        && ./configure --with-recommended-packages \
        && make \
        && make install

CMD ["R"]
