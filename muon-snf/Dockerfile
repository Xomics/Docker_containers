# Dockerfile VERSION = v0.5
# docker login registry.cmbi.umcn.nl
# docker build -t registry.cmbi.umcn.nl/eatris-plus/eatrisplus_omics_tools/muon-snf:$VERSION . 
# docker push registry.cmbi.umcn.nl/eatris-plus/eatrisplus_omics_tools/muon-snf:$VERSION
# sudo docker pull registry.cmbi.umcn.nl/eatris-plus/eatrisplus_omics_tools/muon-snf:$VERSION
# sudo docker images # to get IMAGE_ID
# sudo docker save $IMAGE_ID -o muon-snf.tar
# sudo singularity build muon-snf.sif docker-archive://muon-snf.tar

FROM continuumio/miniconda3

ARG DEBIAN_FRONTEND=noninteractive
ARG BUILD_DATE

LABEL org.label-schema.build-date=$BUILD_DATE
LABEL org.label-schema.vendor="Radboudumc, Medical Biosciences department"
LABEL maintainer="casper.devisser@radboudumc.nl"

WORKDIR /container

ARG DEBIAN_FRONTEND=noninteractive

#Installing git and nano
RUN apt-get update -y 
RUN apt install git
RUN apt install nano

# Installations for Nextflow metrics, 'ps' command
RUN apt-get update && apt-get install -y procps && rm -rf /var/lib/apt/lists/*

#Adding Jupyer notebook and installing conda environment
RUN conda create --name muon
RUN pip install numpy==1.23.1 \
    && pip install muon==0.1.3 \
    && pip install notebook==6.4.10 \
    && pip install snfpy==0.2.2 \
    && pip install pandas==1.4.1 \
    && pip install matplotlib==3.5.2 \
    && pip install papermill==2.4.0 \
    && pip install ipykernel==6.16.0 \
    && pip install statsmodels==0.13.2 \
    && pip install seaborn==0.12.2 \
    && pip install Jinja2==3.1.2 \
    && pip install black==23.3.0 \
    && pip install pyreadr==0.4.7

RUN pip install pySummarizedExperiment

CMD ["/bin/bash"]

ENTRYPOINT ["conda", "run", "--no-capture-output", "-n", "muon", "jupyter", "notebook", "--notebook-dir=/container/", "--ip=*", "--port=8888", "--no-browser", "--allow-root"]