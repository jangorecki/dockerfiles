FROM registry.gitlab.com/jangorecki/dockerfiles/r-builder

MAINTAINER Jan Gorecki j.gorecki@wit.edu.pl

RUN apt-get update -qq \
  && apt-get install -y --no-install-recommends \
    libxml2-dev \
    libfontconfig1-dev \
    libfreetype6-dev libpng-dev libtiff5-dev libjpeg-dev \
    libharfbuzz-dev libfribidi-dev \
    apt-transport-https ca-certificates \
  && apt-get clean \
  && update-ca-certificates \
  && rm -rf /var/lib/apt/lists/*

RUN Rscript -e 'install.packages("pkgdown", repos="https://cloud.r-project.org")'

CMD ["R"]
