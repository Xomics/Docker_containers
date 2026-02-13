# Dockerfile VERSION = v0.1
# docker build --build-arg BUILD_DATE=$(date -u +'%Y-%m-%dT%H:%M:%SZ') -t r-mae-multi-omics-ipsc:$VERSION . 
# docker images # to get IMAGE_ID
# docker save $IMAGE_ID -o r-mae-multi-omics-ipsc.tar
# sudo singularity build r-mae-multi-omics-ipsc.sif docker-archive://r-mae-multi-omics-ipsc.tar


FROM rocker/r-ver:4.4.0

ARG BUILD_DATE

ARG BUILD_DATELABEL org.label-schema.build-date=$BUILD_DATE
LABEL org.label-schema.vendor="Radboudumc, Medical Biosciences department"
LABEL maintainer="casper.devisser@radboudumc.nl"


RUN apt-get -y update && apt-get install -y \
    build-essential \
    cmake \
    pandoc \
    wget \
    libcurl4-openssl-dev \
    libssl-dev \
    libxml2-dev \
    libfontconfig1-dev \
    liblzma-dev \
    libbz2-dev \
    libharfbuzz-dev \
    libfribidi-dev \
    zlib1g-dev \
    libfreetype6-dev \
    libpng-dev \
    libtiff5-dev \
    libjpeg-dev \
    libwebp-dev 

# Install MafDb package
RUN wget https://bioconductor.org/packages/3.19/data/annotation/src/contrib/MafDb.1Kgenomes.phase3.GRCh38_3.10.0.tar.gz \
    && R -e "install.packages('MafDb.1Kgenomes.phase3.GRCh38_3.10.0.tar.gz', repos=NULL, type='source')" \
    && rm MafDb.1Kgenomes.phase3.GRCh38_3.10.0.tar.gz


# Install MultiAssayExperiment package (try different Bioc versions)
RUN wget https://bioconductor.org/packages/3.19/bioc/src/contrib/MultiAssayExperiment_1.30.3.tar.gz \
    && R -e "install.packages('MultiAssayExperiment_1.30.3.tar.gz', repos=NULL, type='source')" \
    && rm MultiAssayExperiment_1.30.3.tar.gz

# Install renv
RUN R -e "install.packages('renv', repos='https://cloud.r-project.org')"

# Copy lockfile
COPY renv.lock renv.lock

# Restore
RUN R -e "renv::restore()"

# Installations for Nextflow metrics, 'ps' command
RUN apt-get update && apt-get install -y procps && rm -rf /var/lib/apt/lists/*