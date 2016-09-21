FROM docker.io/r-base-dev

MAINTAINER Jan Gorecki j.gorecki@wit.edu.pl

RUN apt-get update -qq \
    && apt-get install -y openjdk-8-jdk \
    && rm -rf /var/lib/apt/lists/*

# start R
CMD ["R"]
