FROM docker.io/jangorecki/r-base-dev

MAINTAINER Jan Gorecki j.gorecki@wit.edu.pl

RUN apt-get update -qq \
        && apt-get build-dep -y \
                r-base-dev \
                qpdf \
                r-cran-rgl \
                r-cran-rmpi \
                r-cran-cairodevice \
                r-cran-tkrplot \
        && apt-get install -y \
                git \
                libcurl4-openssl-dev \
                xorg-dev x11-common libgdal-dev libproj-dev mysql-client libcairo2-dev libglpk-dev \
                texlive texlive-latex-extra texlive-bibtex-extra texinfo fonts-inconsolata latex-xcolor \
                libv8-dev \
                gsl-bin libgsl0-dev \
                libgtk2.0-dev netcdf-bin \
                libcanberra-gtk-module \
                openjdk-7-jdk \
                libnetcdf-dev udunits-bin libudunits2-dev \
                tk8.6-dev \
                clustalo \
                texlive-xetex \
                texlive-pstricks \
        && R CMD javareconf \
        && rm -rf /var/lib/apt/lists/*

CMD ["R"]
