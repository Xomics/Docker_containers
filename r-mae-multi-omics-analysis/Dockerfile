# Dockerfile VERSION = v0.1
# docker login registry.cmbi.umcn.nl
# docker build --build-arg BUILD_DATE=$(date -u +'%Y-%m-%dT%H:%M:%SZ') -t registry.cmbi.umcn.nl/eatris-plus/eatrisplus_omics_tools/rstudio-mae-multi-omics-analysis:$VERSION . 
# docker push registry.cmbi.umcn.nl/eatris-plus/eatrisplus_omics_tools/rstudio-mae-multi-omics-analysis:$VERSION
# docker pull registry.cmbi.umcn.nl/eatris-plus/eatrisplus_omics_tools/rstudio-mae-multi-omics-analysis:$VERSION
# docker images # to get IMAGE_ID
# docker save $IMAGE_ID -o rstudio-mae-multi-omics-analysistar
# sudo singularity build rstudio-mae-multi-omics-analysis.sif docker-archive://rstudio-mae-multi-omics-analysis.tar

FROM rocker/rstudio:4.2.2

ARG BUILD_DATE

LABEL org.label-schema.build-date=$BUILD_DATE
LABEL org.label-schema.vendor="Radboudumc, Medical Biosciences department"
LABEL maintainer="casper.devisser@radboudumc.nl"

RUN apt-get -y update && apt-get install -y \
    build-essential \
    cmake \
    pandoc \
    libcurl4-openssl-dev \
    libssl-dev \
    libxml2-dev \
    libfontconfig1-dev \
    r-bioc-rhtslib


# Install R packages
RUN R -e "install.packages('remotes', repos = c(CRAN = 'https://cloud.r-project.org'))"
RUN R -e "install.packages('BiocManager', version = '3.12')" \
        && R -e "BiocManager::install(version = '3.16')" 
RUN R -e "BiocManager::install(c('Bioconductor/GenomeInfoDb', 'Bioconductor/BSgenome'))"

# Install Renv and all packages in the lock file
ENV RENV_VERSION 0.15.2-2
RUN R -e "remotes::install_github('rstudio/renv@${RENV_VERSION}')"
COPY renv.lock renv.lock
RUN R -e 'renv::restore()'

# Installations for Nextflow metrics, 'ps' command
RUN apt-get update && apt-get install -y procps && rm -rf /var/lib/apt/lists/*