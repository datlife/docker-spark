FROM continuumio/miniconda3

ENV SPARK_VERSION           2.4.0
ENV BASE_DIR                /opt
ENV NOTEBOOKS_HOME          ${BASE_DIR}/notebooks
ENV SPARK_HOME              ${BASE_DIR}/spark
ENV PYSPARK_DRIVER_PYTHON   ipython
ENV PATH                    ${SPARK_HOME}/bin:${SPARK_HOME}/sbin:${PATH}

# Python Packages
RUN conda install --yes \
    numpy pandas matplotlib scikit-learn jupyter ipython \
    pyspark=${SPARK_VERSION} pyarrow && \
    conda clean -tipsy && \
    mkdir -p ${NOTEBOOKS_HOME}

# OpenJDK
RUN apt-get update --fix-missing && \
    apt-get install -y openjdk-8-jdk-headless procps && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Spark
RUN curl -s https://archive.apache.org/dist/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop2.7.tgz | tar xz -C /tmp && \
    mv /tmp/spark-${SPARK_VERSION}-bin-hadoop2.7 ${SPARK_HOME}

WORKDIR ${BASE_DIR}/work
