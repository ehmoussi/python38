FROM centos:centos7

# install needed packages
RUN yum install -y \
        yum-utils \
        curl \
        git \
        gcc && \
    yum groupinstall -y "Development Tools" && \
    yum install -y \
        openssl-devel
RUN yum clean -y all

# Download and install Python 3.8
RUN curl https://www.python.org/ftp/python/3.8.5/Python-3.8.5.tgz -O -J -L && \
    tar xzf Python-3.8.5.tgz -C /usr/src/ && \
    /usr/src/Python-3.8.5/configure --enable-optimizations --prefix=/usr/bin/python3 && \
    make altinstall && \
    ln -s /usr/bin/python3/bin/python3.8 /usr/bin/python3.8 && \
    rm Python-3.8.5.tgz

# set python3.8 as default
RUN alternatives --install /usr/bin/unversioned-python python /usr/bin/python3.8 70
RUN alternatives --set python /usr/bin/python3.8
RUN rm -rf /usr/bin/python && ln -s /usr/bin/unversioned-python /usr/bin/python
# Add python binaries to the PATH
ENV PATH=/usr/bin/python3/bin:$PATH

# symlink pip
RUN ln -s /usr/bin/python3/bin/pip3.8 /usr/bin/pip
RUN pip --version && pip install --upgrade pip 'pipenv<2020.5.28' setuptools wheel
RUN ln -s /usr/bin/python3/bin/pipenv /usr/bin/pipenv

