FROM docker.io/ubuntu:16.04

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
        && rm -rf /var/lib/apt/lists/*

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN add-apt-repository "deb https://cloud.r-project.org/bin/linux/ubuntu $(lsb_release -cs)/" \
        && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9

RUN apt-get update -qq \
        && apt-get install -y --no-install-recommends \
                r-base-dev \
                r-recommended \
        && echo 'options(repos = c(CRAN = "https://cloud.r-project.org"), download.file.method = "libcurl")' >> /etc/R/Rprofile.site \
        && rm -rf /var/lib/apt/lists/*

CMD ["R"]
