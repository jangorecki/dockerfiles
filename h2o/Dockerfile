FROM jangorecki/r-base-dev

MAINTAINER Jan Gorecki j.gorecki@wit.edu.pl

RUN apt-get update -qq \
        && apt-get -y install debconf-utils

RUN add-apt-repository -y ppa:webupd8team/java

RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections

RUN apt-get update -qq \
        && apt-get -y install oracle-java8-installer \
                oracle-java8-set-default \
        && rm -rf /var/lib/apt/lists/*

RUN Rscript -e 'install.packages("h2o")'

CMD ["R"]
