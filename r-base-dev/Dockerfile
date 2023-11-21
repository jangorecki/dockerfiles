FROM ubuntu:22.04

MAINTAINER Jan Gorecki j.gorecki@wit.edu.pl

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update -qq \
        && apt-get upgrade -y

RUN apt-get install -y --install-recommends \
                apt-transport-https \
                software-properties-common \
                apt-utils \
                ca-certificates \
                dirmngr

RUN apt-get install -y --no-install-recommends \
                curl \
                wget \
                git \
                libssl-dev \
                libcurl4-gnutls-dev \
                vim \
                locales \
                dbus \
                qpdf \
                devscripts \
        && rm -rf /var/lib/apt/lists/*

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN add-apt-repository -n "deb https://cloud.r-project.org/bin/linux/ubuntu $(lsb_release -cs)-cran40/" \
        && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9

RUN apt-get update -qq \
        && apt-get install -y --no-install-recommends \
                r-base-dev \
                r-recommended \
        && rm -rf /var/lib/apt/lists/*

RUN echo 'options(repos=c(CRAN="https://cloud.r-project.org"))' >> /etc/R/Rprofile.site

CMD ["R"]
