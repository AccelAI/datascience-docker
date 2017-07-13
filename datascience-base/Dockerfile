FROM ubuntu:latest

MAINTAINER Accel.ai <info@accel.ai>

ENV DEBIAN_FRONTEND noninteractive

ENV LANGUAGE en_US.UTF-8
ENV LANG en_US.UTF-8

# Install packages ... change the timezone line if you're not in Pacific time
RUN apt-get -y update && apt-get install -y wget nano bzip2 locales curl unzip wget openssl libhdf5-dev libpq-dev tzdata vim git \
    && apt-get clean && dpkg-reconfigure locales && locale-gen en_US.UTF-8 \
    && echo "America/Los_Angeles" > /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata \
    && apt-get autoremove \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


# Install and setup minimal Anaconda Python distribution, then tear down temp files
# Additional libs left out to save space : cython hdf5 pytables nltk scikit-image
RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh \
    && wget --quiet https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3.sh \
    && /bin/bash ~/miniconda3.sh -b -p /opt/conda \
    && mkdir /opt/notebooks \
    && /opt/conda/bin/conda install scipy scikit-learn nose readline pandas seaborn jupyter \
       tk graphviz requests pyyaml setuptools pip ipywidgets tensorflow keras pytorch theano \
    && /opt/conda/bin/conda clean -i -l -t -y \
    && rm ~/miniconda3.sh

# Get the pip packages and clean up
ADD requirements.txt /
RUN /opt/conda/bin/pip install -r /requirements.txt && rm -rf /root/.cache/pip/*

RUN apt-get install -y curl grep sed dpkg && \
    TINI_VERSION=`curl https://github.com/krallin/tini/releases/latest | grep -o "/v.*\"" | sed 's:^..\(.*\).$:\1:'` && \
    curl -L "https://github.com/krallin/tini/releases/download/v${TINI_VERSION}/tini_${TINI_VERSION}.deb" > tini.deb && \
    dpkg -i tini.deb && \
    rm tini.deb && \
    apt-get clean

ENV PATH /opt/conda/bin:$PATH

ENV PEM_FILE /key.pem
# $PASSWORD will get `unset` within notebook.sh, turned into an IPython style hash
ENV PASSWORD teamaccelai
ENV USE_HTTP 1

# Add current files to / and set entry point.
#ADD /opt/notebooks
WORKDIR /opt/notebooks
ADD notebook.sh /notebook.sh
RUN chmod a+x /notebook.sh

EXPOSE 8888
ENTRYPOINT [ "/usr/bin/tini", "--" ]
CMD [ "/bin/bash" ]

