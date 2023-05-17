# Dockerfile VERSION = v0.1
# docker login registry.cmbi.umcn.nl
# docker build --build-arg BUILD_DATE=$(date -u +'%Y-%m-%dT%H:%M:%SZ') -t registry.cmbi.umcn.nl/eatris-plus/eatrisplus_omics_tools/rstudio_server:$VERSION . 
# docker push registry.cmbi.umcn.nl/eatris-plus/eatrisplus_omics_tools/rstudio_server:$VERSION

FROM rocker/rstudio:4.3.0

ARG BUILD_DATE

LABEL org.label-schema.build-date=$BUILD_DATE
LABEL org.label-schema.vendor="Radboudumc, Medical Biosciences department"
LABEL maintainer="casper.devisser@radboudumc.nl"

RUN R -e "install.packages('ggplot2')" 