FROM docker.io/ubuntu:16.04

## this image makes it ready to build h2o, it uses R 3.3.0:
# git clone https://github.com/h2oai/h2o-3.git
# cd h2o-3
# ./gradlew syncSmalldata
# Rscript -e 'install.packages("kernlab")' # syncRPackages fails to install kernlab for R 3.3.0 from h2o repo, this uses CRAN version
# ./gradlew syncRPackages
# ./gradlew build

MAINTAINER Jan Gorecki j.gorecki@wit.edu.pl

RUN apt-get update -qq \
        && apt-get upgrade -y

# core utils

RUN apt-get update -qq \
        && apt-get install -y --no-install-recommends \
                apt-transport-https \
                software-properties-common \
                curl \
                git \
                libssl-dev \
                libcurl4-gnutls-dev \
                vim \
        && rm -rf /var/lib/apt/lists/*

# locale

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# Node.js

RUN curl -sL https://deb.nodesource.com/setup_0.12 | bash -

RUN apt-get install -y \
                nodejs  \
                npm

RUN ln -s "$(which nodejs)" /usr/bin/node

RUN echo '{ "allow_root": true }' >> /root/.bowerrc

# R

RUN add-apt-repository "deb https://cran.rstudio.com/bin/linux/ubuntu $(lsb_release -cs)/" \
        && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9

RUN apt-get update -qq \
        && apt-get install -y --no-install-recommends \
                r-base-dev \
                r-recommended \
        && echo 'options(repos = c(CRAN = "https://cran.rstudio.com/"), download.file.method = "libcurl")' >> /etc/R/Rprofile.site \
        && rm -rf /var/lib/apt/lists/*

RUN apt-get build-dep -y r-cran-rgl

RUN apt-get install -y libxml2-dev

# Java

RUN add-apt-repository -y ppa:webupd8team/java

RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections

RUN apt-get update -qq \
        && apt-get -y install oracle-java8-installer \
                oracle-java8-set-default \
        && rm /var/cache/oracle-jdk8-installer/jdk-* \
        && apt-get install -f \
        && rm -rf /var/lib/apt/lists/*


# Python

RUN apt-get install python-pip

RUN pip install requests future tabulate

# run

CMD ["/bin/bash"]
