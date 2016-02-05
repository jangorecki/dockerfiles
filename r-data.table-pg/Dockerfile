FROM jangorecki/r-data.table

MAINTAINER Jan Gorecki j.gorecki@wit.edu.pl

# install postgres native drivers
RUN apt-get update -qq \
 && apt-get install -y --no-install-recommends libpq-dev

# setup R repos
RUN echo 'options(repos = paste0("https://", c("cran.rstudio.com","olafmersmann.github.io/drat","jangorecki.github.io/logR","jangorecki.github.io/pg")))' >> /etc/R/Rprofile.site

# install R packages
RUN Rscript -e 'install.packages(c("RPostgreSQL","microbenchmarkCore","logR","pg"))'

# expose Rserve port
EXPOSE 6311

# start Rserve
CMD ["R","CMD","Rserve","--RS-conf","/etc/Rserve.conf","--no-save"]
