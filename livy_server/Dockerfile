FROM datworks/spark

# Set install path for Livy
# ENV LIVY_BUILD_VERSION livy-0.5.0-incubating-bin
ENV LIVY_HOME /apps/livy
ENV LIVY_LOG $LIVY_HOME/logs

RUN apt-get -y update --fix-missing && \
    apt-get install --no-install-recommends -y unzip maven libkrb5-dev gcc python-dev && \
    apt-get clean

# Clone Livy repository
#RUN mkdir -p /apps && \
#    cd /apps && \
#    wget https://www-us.apache.org/dist/incubator/livy/0.5.0-incubating/livy-0.5.0-incubating-bin.zip && \
ENV LIVY_BUILD_VERSION 0.6.0-incubating
ENV LIVY_BUILD_PATH /apps/build/incubator-livy


RUN conda create -n py2 python=2.7
RUN . /opt/conda/etc/profile.d/conda.sh && \
    conda deactivate &&\
    conda activate py2 && \
    mkdir -p /apps mkdir -p /apps/build && \
    cd /apps/build && \
    git clone https://github.com/apache/incubator-livy && cd incubator-livy && \
    git checkout v0.6.0-incubating && \
    mvn -Dmaven.test.skip=true package

RUN unzip $LIVY_BUILD_PATH/assembly/target/apache-livy-${LIVY_BUILD_VERSION}-bin.zip -d /apps && \
    cd /apps && \
    mv /apps/apache-livy-0.6.0-incubating-bin /apps/livy &&\
    rm -rf $LIVY_BUILD_PATH

#    wget https://github.com/apache/incubator-livy/archive/v0.6.0-incubating.zip &&\
#    unzip $LIVY_BUILD_VERSION.zip && \
#    mv incubator-livy-0.6.0-incubating  $LIVY_HOME && \
#    rm /apps/$LIVY_BUILD_VERSION.zip && \
#    mkdir -p $LIVY_LOG

COPY livy.conf $LIVY_HOME/conf
RUN mkdir -p /apps/spark-modules
