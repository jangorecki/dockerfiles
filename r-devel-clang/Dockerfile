FROM silkeh/clang:11

MAINTAINER Jan Gorecki <j.gorecki@wit.edu.pl>

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
ENV LC_ALL C

RUN add-apt-repository -s "deb https://cloud.r-project.org/bin/linux/debian $(lsb_release -cs)-cran40/" \
        && apt-key adv --keyserver keys.gnupg.net --recv-key 'E19F5F87128899B192B1A2C2AD5F960A256A04AF'

RUN apt-get update -qq \
        && apt-get -y --no-install-recommends \
                build-dep \
                r-base-dev \
        && rm -rf /var/lib/apt/lists/*

RUN curl -O https://stat.ethz.ch/R/daily/R-devel.tar.gz \
        && tar xvf R-devel.tar.gz \
        && cd R-devel/ \
        && ./configure --without-recommended-packages \
        && make \
        && make install

RUN mkdir -p ~/.R \
        && echo 'CC=clang\nCXX=clang++' > ~/.R/Makevars \
        && echo 'CFLAGS=-g -O3 -Wall -pedantic\nFFLAGS=-g -O2 -mtune=native -Wall -pedantic' >> ~/.R/Makevars \
        && echo 'CXXFLAGS=-g -O3 -Wall -pedantic -frtti\nCPPFLAGS=-isystem /usr/local/clang/include' >> ~/.R/Makevars \
        && echo 'JAVA_HOME=/usr/lib/jvm/java-1.8.0\nLDFLAGS=-L/usr/local/clang/lib64 -L/usr/local/lib64' >> ~/.R/Makevars

RUN echo 'options(repos = c(CRAN = "https://cloud.r-project.org"), download.file.method = "libcurl")' >> /usr/local/lib/R/etc/Rprofile.site

CMD ["R"]

