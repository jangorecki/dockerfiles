FROM registry.gitlab.com/jangorecki/dockerfiles/r-base-dev

MAINTAINER Jan Gorecki j.gorecki@wit.edu.pl

# install qpdf for R check
RUN apt-get update -qq \
  && apt-get install -y --no-install-recommends qpdf \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

# install latex required for building sweave vignettes and pdf manual
# https://github.com/rocker-org/hadleyverse/blob/master/Dockerfile
RUN apt-get update -qq \
  && apt-get install -y --no-install-recommends \
    aspell \
    aspell-en \
    ghostscript \
    imagemagick \
    lmodern \
    texlive-fonts-recommended \
    texlive-humanities \
    texlive-latex-extra \
    texinfo \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && cd /usr/share/texlive/texmf-dist \
  && wget http://mirrors.ctan.org/install/fonts/inconsolata.tds.zip \
  && unzip inconsolata.tds.zip \
  && rm inconsolata.tds.zip \
  && echo "Map zi4.map" >> /usr/share/texlive/texmf-dist/web2c/updmap.cfg \
  && mktexlsr \
  && updmap-sys

# install pandoc required for building markdown vignettes
RUN wget https://github.com/jgm/pandoc/releases/download/2.2/pandoc-2.2-1-amd64.deb \
  && dpkg -i pandoc-2.2-1-amd64.deb \\
  && rm pandoc-2.2-1-amd64.deb

# start R
CMD ["R"]
