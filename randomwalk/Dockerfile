FROM continuumio/miniconda3

RUN conda create --name multixrank python=3.10 -y
RUN python3 -m pip install multixrank
RUN python3 -m pip install scipy==1.8

WORKDIR /random_walk/

#to COPY the remote file at working directory in container
COPY multiXrank_covid_full_4-layers_PCC_0.1_threshold_mild.py ./random_walk/
COPY config_full_covid_4-layers_PCC_0.1_threshold_mild.yml ./random_walk/
COPY multiXrank_full_4-layers_PCC_0.1_threshold_mild.sh ./random_walk/

CMD [ "sbatch", "./bash.sh"  "]