FROM docker.io/jangorecki/r-base-dev

MAINTAINER Jan Gorecki j.gorecki@wit.edu.pl

# setup R repos
RUN echo 'options(repos = c("https://cran.rstudio.com","http://rforge.net","https://Rdatatable.github.io/data.table"))' >> /etc/R/Rprofile.site

# install R packages
RUN Rscript -e 'install.packages(c("RSclient","Rserve","data.table"))'

# Rserv.conf
RUN echo 'remote enable' >> /etc/Rserve.conf \
 && echo 'auth disable' >> /etc/Rserve.conf \
 && echo 'fileio enable' >> /etc/Rserve.conf \
 && echo 'maxinbuf 500000' >> /etc/Rserve.conf \
 && echo 'encoding utf8' >> /etc/Rserve.conf \
 && echo 'daemon enable' >> /etc/Rserve.conf

# expose Rserve port
EXPOSE 6311

# start Rserve
CMD R CMD Rserve --RS-conf /etc/Rserve.conf --no-save && /bin/sh -c "while true; do sleep 5; done;"
