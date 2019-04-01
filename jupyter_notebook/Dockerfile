FROM datworks/spark

# Install required packages to have functional notebook
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - && \
    apt-get update && apt-get install -yq --no-install-recommends \
    build-essential \
    emacs \
    git \
    inkscape \
    jed \
    libsm6 \
    libxext-dev \
    libxrender1 \
    lmodern \
    netcat \
    pandoc \
    python-dev \
    libkrb5-dev \
    texlive-fonts-extra \
    texlive-fonts-recommended \
    texlive-generic-recommended \
    texlive-latex-base \
    texlive-latex-extra \
    texlive-xetex \
    tzdata \
    npm nodejs \
    && rm -rf /var/lib/apt/lists/*


# Install Jupyter Notebook, Lab, and Hub
# # Generate a notebook server config
RUN conda install --yes \
    'notebook=5.7.8' \
    'jupyterlab=0.35.4'\
    'tornado=4.5.3' &&\
    pip install sparkmagic==0.12.1 && \
    conda clean -tipsy && \
    npm cache clean --force && \
    jupyter notebook --generate-config && \
    rm -rf $CONDA_DIR/share/jupyter/lab/staging && \
    rm -rf ~/.cache/yarn && \
    mkdir ~/.sparkmagic

# ======================
# Install Jupyter Kernel
# ======================
WORKDIR /opt/conda/lib/python3.7/site-packages
RUN  jupyter-kernelspec install sparkmagic/kernels/pysparkkernel && \
     jupyter-kernelspec install sparkmagic/kernels/pyspark3kernel && \
     jupyter nbextension enable --py widgetsnbextension --sys-prefix && \
     jupyter serverextension enable --py sparkmagic

COPY config.json /root/.sparkmagic/config.json
WORKDIR /opt/notebooks

