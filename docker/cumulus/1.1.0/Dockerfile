FROM debian:buster-slim
SHELL ["/bin/bash", "-c"]

RUN mkdir -p /usr/share/man/man1 && \
    apt-get -qq update && \
    apt-get -qq -y install --no-install-recommends \
        build-essential \
        automake \
        zlib1g-dev \
        libxml2-dev \
        cmake \
        gnupg \
        libfftw3-dev \
        default-jdk \
        curl \
        python3 \
        python3-dev \
        python3-pip

RUN echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] http://packages.cloud.google.com/apt cloud-sdk main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key --keyring /usr/share/keyrings/cloud.google.gpg  add - && \
    apt-get update -y && apt-get install -y google-cloud-sdk=319.0.0-0

RUN ln -s /usr/bin/python3 /usr/bin/python

RUN python -m pip install --upgrade pip --no-cache-dir && \
    python -m pip install setuptools==51.0.0 --no-cache-dir && \
    python -m pip install numpy==1.19.4 --no-cache-dir && \
    python -m pip install pandas==1.1.5 --no-cache-dir && \
    python -m pip install scipy==1.5.4 --no-cache-dir && \
    python -m pip install Cython==0.29.21 --no-cache-dir && \
    python -m pip install pybind11==2.6.1 --no-cache-dir && \
    python -m pip install scikit-image==0.17.2 --no-cache-dir && \
    python -m pip install scikit-learn==0.23.2 --no-cache-dir && \
    python -m pip install h5py==3.1.0 --no-cache-dir && \
    python -m pip install fitsne==1.1.1 --no-cache-dir && \
    python -m pip install importlib-metadata==3.1.1 --no-cache-dir && \
    python -m pip install joblib==0.17.0 --no-cache-dir && \
    python -m pip install python-igraph==0.8.3 --no-cache-dir && \
    python -m pip install leidenalg==0.8.3 --no-cache-dir && \
    python -m pip install lightgbm==3.1.0 --no-cache-dir && \
    python -m pip install llvmlite==0.35.0 --no-cache-dir && \
    python -m pip install loompy==3.0.6 --no-cache-dir && \
    python -m pip install matplotlib==3.3.3 --no-cache-dir && \
    python -m pip install natsort==7.1.0 --no-cache-dir && \
    python -m pip install numba==0.52.0 --no-cache-dir && \
    python -m pip install scanorama==1.7 --no-cache-dir && \
    python -m pip install scikit-misc==0.1.3 --no-cache-dir && \
    python -m pip install seaborn==0.11.0 --no-cache-dir && \
    python -m pip install statsmodels==0.12.1 --no-cache-dir && \
    python -m pip install numcodecs==0.7.2 --no-cache-dir && \
    python -m pip install networkx==2.5 --no-cache-dir && \
    python -m pip install zarr==2.6.1 --no-cache-dir && \
    python -m pip install anndata==0.7.5 --no-cache-dir && \
    python -m pip install hnswlib==0.4.0 --no-cache-dir && \
    python -m pip install louvain==0.7.0 --no-cache-dir && \
    python -m pip install MulticoreTSNE-modified==0.1 --no-cache-dir && \
    python -m pip install umap-learn==0.4.6 --no-cache-dir && \
    python -m pip install torch==1.7.0 --no-cache-dir && \
    python -m pip install harmony-pytorch==0.1.4 --no-cache-dir && \
    python -m pip install cirrocumulus==1.1.11.post1 --no-cache-dir && \
    python -m pip install annoy==1.17.0 --no-cache-dir && \
    python -m pip install pegasusio==0.2.8 --no-cache-dir && \
    python -m pip install demuxEM==0.1.5 --no-cache-dir && \
    python -m pip install pegasuspy==1.1.0 --no-cache-dir

RUN mkdir /software && \
    cp /usr/local/lib/python3.7/dist-packages/cirrocumulus/prepare_data.py /software/prepare_data.py

RUN apt-get -qq -y remove curl gnupg cmake && \
    apt-get -qq -y autoremove && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /var/log/dpkg.log

ADD https://raw.githubusercontent.com/klarman-cell-observatory/cumulus/master/docker/monitor_script.sh /software
RUN chmod a+rx /software/monitor_script.sh

ENV PATH=/software:$PATH
