FROM continuumio/anaconda3
RUN apt-get update && apt-get install -y libgtk2.0-dev && \
    rm -rf /var/lib/apt/lists/*
RUN /opt/conda/bin/conda update -n base -c defaults conda && \
    /opt/conda/bin/conda install python && \
    /opt/conda/bin/conda install anaconda-client && \
    /opt/conda/bin/conda install numpy pandas matplotlib -y && \
    /opt/conda/bin/conda install -c conda-forge jupyterlab -y && \
    /opt/conda/bin/conda upgrade dask

# install pygmt
# RUN /opt/conda/bin/conda install mamba -n base -c conda-forge -y

RUN /opt/conda/bin/conda create -n pygmt -c conda-forge pygmt -y

RUN python -m ipykernel install --user --name pygmt

RUN /opt/conda/bin/conda init bash

RUN /opt/conda/bin/conda activate pygmt

RUN ["mkdir", "notebooks"]

COPY conf/.jupyter /root/.jupyter

COPY run_jupyter.sh /

EXPOSE 8888

VOLUME /notebooks

CMD ["/run_jupyter.sh"]
