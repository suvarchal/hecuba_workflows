FROM continuumio/miniconda3:latest
RUN apt-get update && apt-get install -y \
  automake \
  build-essential \
  curl \
  cmake \
  git \
  libtool \
  libuv1 \
  m4 \
  && rm -rf /var/lib/apt/lists/*
# only upto python 3.8 is supported for arrow=0.15.1 
RUN conda install python=3.8
RUN conda install -c conda-forge \
  pyarrow=0.15.1 \
  tbb=2020.0 \
  zlib \
  && conda clean -afy

RUN git clone https://github.com/bsc-dd/hecuba.git
WORKDIR  /hecuba
ENV LD_LIBRARY_PATH=/opt/conda/lib
ENV C_INCLUDE_PATH=/opt/conda/include
RUN python setup.py install --c_binding=/opt/conda
WORKDIR  /
RUN rm -rf /hecuba
