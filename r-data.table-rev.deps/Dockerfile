FROM docker.io/jangorecki/r-base-dev

MAINTAINER Jan Gorecki j.gorecki@wit.edu.pl

# install pandoc required for 'sdcMicro' package
RUN PANDOC_VERSION='1.13.1' \
  && PANDOC_DIR="${HOME}/opt/pandoc" \
  && PANDOC_URL="https://s3.amazonaws.com/rstudio-buildtools/pandoc-${PANDOC_VERSION}.zip" \
  && mkdir -p "${PANDOC_DIR}" \
  && curl -o /tmp/pandoc-${PANDOC_VERSION}.zip ${PANDOC_URL} \
  && unzip -j /tmp/pandoc-${PANDOC_VERSION}.zip "pandoc-${PANDOC_VERSION}/linux/debian/x86_64/pandoc" -d "${PANDOC_DIR}" \
  && chmod +x "${PANDOC_DIR}/pandoc" \
  && ln -s "${PANDOC_DIR}/pandoc" /usr/local/bin \
  && unzip -j /tmp/pandoc-${PANDOC_VERSION}.zip "pandoc-${PANDOC_VERSION}/linux/debian/x86_64/pandoc-citeproc" -d "${PANDOC_DIR}" \
  && chmod +x "${PANDOC_DIR}/pandoc-citeproc" \
  && ln -s "${PANDOC_DIR}/pandoc-citeproc" /usr/local/bin

RUN apt-get update -qq \
        && apt-get build-dep -y \
                r-base-dev \
                qpdf \
                r-cran-rgl \
                r-cran-rmpi \
                r-cran-cairodevice \
                r-cran-tkrplot \
        && apt-get install -y \
                qpdf \
                libcurl4-openssl-dev \
                xvfb xauth xfonts-base r-cran-rgtk2 \
                xorg-dev x11-common libgdal-dev libproj-dev mysql-client libcairo2-dev libglpk-dev \
                texlive texlive-latex-extra texlive-bibtex-extra texinfo fonts-inconsolata latex-xcolor \
                libv8-dev \
                gsl-bin libgsl0-dev \
                libgtk2.0-dev netcdf-bin \
                libcanberra-gtk-module \
                openjdk-8-jdk \
                libnetcdf-dev udunits-bin libudunits2-dev \
                tk8.6-dev \
                clustalo \
                texlive-xetex \
                texlive-pstricks \
                libfftw3-dev \
        && R CMD javareconf \
        && rm -rf /var/lib/apt/lists/*

# R check envs
ENV _R_CHECK_CRAN_INCOMING_=FALSE
ENV _R_CHECK_FORCE_SUGGESTS_=FALSE

CMD ["/bin/bash"]
