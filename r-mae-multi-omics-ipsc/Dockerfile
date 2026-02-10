# Dockerfile VERSION = v0.1
# docker build --build-arg BUILD_DATE=$(date -u +'%Y-%m-%dT%H:%M:%SZ') -t r-mae-multi-omics-ipsc:$VERSION . 
# docker images # to get IMAGE_ID
# docker save $IMAGE_ID -o r-mae-multi-omics-ipsc.tar
# sudo singularity build r-mae-multi-omics-ipsc.sif docker-archive://r-mae-multi-omics-ipsc.tar

FROM r-base:4.4.0

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
    libfontconfig1-dev 


# Install Renv and all packages in the lock file
RUN R -e "remotes::install_github('rstudio/renv@1.1.5')"
COPY renv.lock renv.lock
RUN R -e 'renv::restore()'

# Installations for Nextflow metrics, 'ps' command
RUN apt-get update && apt-get install -y procps && rm -rf /var/lib/apt/lists/*