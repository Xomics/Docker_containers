# Dockerfile VERSION = v0.1
# docker login registry.cmbi.umcn.nl
# docker build -t registry.cmbi.umcn.nl/eatris-plus/eatrisplus_omics_tools/muon:$VERSION . 
# docker push registry.cmbi.umcn.nl/eatris-plus/eatrisplus_omics_tools/muon:$VERSION
# sudo docker pull registry.cmbi.umcn.nl/eatris-plus/eatrisplus_omics_tools/muon$VERSION
# sudo docker images # to get IMAGE_ID
# sudo docker save $IMAGE_ID -o muon.tar
# sudo singularity build muon.sif docker-archive://muon.tar

FROM continuumio/miniconda3
ARG DEBIAN_FRONTEND=noninteractive

LABEL build_data="13-03-2023"
LABEL vendor="Radboudumc, Medical Biosciences department"
LABEL usage=""
LABEL url=""

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
RUN pip install muon==0.1.3 \
    && pip install notebook==6.4.10 \
    && pip install ipykernel==6.12.1

CMD ["/bin/bash"]

ENTRYPOINT ["conda", "run", "--no-capture-output", "-n", "muon", "jupyter", "notebook", "--notebook-dir=/container/", "--ip=*", "--port=8888", "--no-browser", "--allow-root"]