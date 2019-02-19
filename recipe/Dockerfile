FROM centos:6.10
LABEL author="Billy Poon <bkpoon@lbl.gov>"

# add EPEL repository
RUN yum -y install wget && \
    wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm && \
    rpm -ivh epel-release-latest-6.noarch.rpm

# add dependenices from build.sh
RUN yum -y upgrade && \
    yum -y install gtk+-devel gtk+extra-devel gtk2-devel gtk2-engines-devel \
    gtkglext-devel wxGTK-devel wxBase \
    gcc gcc-c++

# install miniconda2 and create build environment
RUN wget https://repo.anaconda.com/miniconda/Miniconda2-latest-Linux-x86_64.sh && \
    /bin/sh Miniconda2-latest-Linux-x86_64.sh -b -u -p /opt/conda && \
    export PATH=/opt/conda/bin:$PATH && \
    conda create -n build --channel conda-forge conda-build conda-verify

ENV PATH /opt/conda/envs/build/bin:$PATH

# copy over recipe
COPY meta.yaml .
COPY build.sh .
COPY .condarc /root/.condarc
RUN mkdir -p /opt/recipe && \
    mv meta.yaml /opt/recipe/meta.yaml && \
    mv build.sh /opt/recipe/build.sh

# run conda build
RUN cd /opt/recipe && \
    conda build .
