FROM ubuntu:20.04

MAINTAINER yuhao<yqyuhao@outlook.com>

#RUN sed -i 's/http:\/\/archive\.ubuntu\.com\/ubuntu\//http:\/\/mirrors\.aliyun\.com\/ubuntu\//g' /etc/apt/sources.list
RUN sed -i 's/http:\/\/archive\.ubuntu\.com\/ubuntu\//http:\/\/mirrors\.aliyun\.com\/ubuntu\//g' /etc/apt/sources.list

# set timezone
RUN set -x 
RUN export DEBIAN_FRONTEND=noninteractive 
RUN apt-get update 
RUN apt-get install -y tzdata 
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai  /etc/localtime 
RUN echo "Asia/Shanghai" > /etc/timezone

# install packages
#RUN apt-get update

RUN apt-get install -y less curl apt-utils vim wget gcc-7 g++-7 make cmake git unzip dos2unix libncurses5 

# lib
RUN apt-get install -y zlib1g-dev libjpeg-dev libncurses5-dev libbz2-dev liblzma-dev libcurl4-gnutls-dev 
 
# python3 perl java r-base
RUN apt-get install -y python3 python3-dev python3-pip python perl openjdk-8-jdk r-base r-base-dev

ENV software /yqyuhao

# conda v4.12
WORKDIR $software/source
RUN wget -c http://10.0.2.251:90/biosoft/scrnaseq/Miniconda3-py37_4.12.0-Linux-x86_64.sh -O $software/source/Miniconda3-py37_4.12.0-Linux-x86_64.sh \
&& sh $software/source/Miniconda3-py37_4.12.0-Linux-x86_64.sh -b -p $software/bin/conda-v4.12 \
&& $software/bin/conda-v4.12/bin/conda config --add channels conda-forge \
&& $software/bin/conda-v4.12/bin/conda config --add channels r \
&& $software/bin/conda-v4.12/bin/conda config --add channels bioconda \
&& $software/bin/conda-v4.12/bin/conda install cutadapt

# cutadapt
#conda install cutadapt

# fastp v 0.22.0
WORKDIR $software/source
RUN wget -c http://10.0.2.251:90/biosoft/pipeline/fastp-0.22.0.tar.gz -O $software/source/fastp.v0.22.0.tar.gz \
&& tar -xf fastp.v0.22.0.tar.gz && cd $software/source/fastp-0.22.0 && make \

# fastqc
WORKDIR $software/source
RUN wget -c http://10.0.2.251:90/biosoft/scrnaseq/fastqc_v0.11.9.zip -O $software/source/fastqc_v0.11.9.zip \
&& unzip $software/source/fastqc_v0.11.9.zip \
&& cd $software/source/FastQC \
&& apt-get install -y fastqc 

# subread
WORKDIR $software/source
RUN wget -c http://10.0.2.251:90/biosoft/scrnaseq/subread-1.5.1-Linux-x86_64.tar.gz -O $software/source/subread-1.5.1-Linux-x86_64.tar.gz \
&& tar -xf $software/source/subread-1.5.1-Linux-x86_64.tar.gz \
&& cd $software/source/subread-1.5.1-Linux-x86_64 
#&& ln -s $software/source/FastQC-0.11.9/fastqc /usr/bin/fastqc

# STAR
WORKDIR $software/source
RUN wget -c http://10.0.2.251:90/biosoft/scrnaseq/STAR -O $software/source/STAR \
&& ln -s $software/source/STAR /usr/bin/STAR

WORKDIR $software/source
RUN rm -Rf fastp.v0.22.0.tar.gz fastqc_v0.11.9.zip subread-1.5.1-Linux-x86_64.tar.gz

# chown root:root
WORKDIR $software/source
RUN chown root:root -R $software/source

