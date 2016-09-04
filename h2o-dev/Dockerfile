FROM docker.io/ubuntu:16.04

## this image makes it ready to build h2o, it use recent R version:
# git clone --depth 1 https://github.com/h2oai/h2o-3.git
# cd h2o-3
# ./gradlew syncSmalldata
# Rscript -e 'install.packages("kernlab")' # syncRPackages fails to install kernlab for recent R from h2o repo, this uses CRAN version
# ./gradlew syncRPackages # kernlab install error, installed from CRAN
# ./gradlew clean
## either of two builds
# ./gradlew build -x test
# (export BUILD_HADOOP=1; ./gradlew build -x test)
# cp /h2o-3/h2o-hadoop/h2o-hdp2.2-assembly/build/libs/h2odriver.jar h2o.jar
# cp /h2o-3/h2o-r/R/src/contrib/h2o_3.11.0.99999.tar.gz h2o.tar.gz

MAINTAINER Jan Gorecki j.gorecki@wit.edu.pl

RUN apt-get update -qq \
        && apt-get upgrade -y

# core utils

RUN apt-get update -qq \
        && apt-get install -y --no-install-recommends \
                apt-transport-https \
                software-properties-common \
                curl \
                wget \
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

RUN apt-get update -qq \
        && apt-get build-dep -y r-cran-rgl

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

RUN apt-get update -qq \
        && apt-get -y install python-pip

RUN pip install requests future tabulate colorama

# run

CMD ["/bin/bash"]
