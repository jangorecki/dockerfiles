FROM docker.io/ubuntu:16.04

MAINTAINER Jan Gorecki j.gorecki@wit.edu.pl

RUN useradd docker \
	&& mkdir /home/docker \
	&& chown docker:docker /home/docker \
	&& addgroup docker staff

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

ENV R_BASE_VERSION 3.4.4

RUN curl -O https://cran.r-project.org/src/base/R-3/R-${R_BASE_VERSION}.tar.gz \
        && tar xvf R-${R_BASE_VERSION}.tar.gz \
        && cd R-${R_BASE_VERSION}/ \
        && ./configure --with-recommended-packages --enable-memory-profiling \
        && make \
        && make install

RUN echo 'options(repos = c(CRAN = "https://cloud.r-project.org"), download.file.method = "libcurl")' >> ~/.Rprofile

RUN echo 'LC_ALL=C' >> ~/.Renviron

CMD ["R"]
