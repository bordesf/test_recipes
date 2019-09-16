Bootstrap: docker
From: pytorch/pytorch:1.0.1-cuda10.0-cudnn7-runtime

%post
        export PATH=$PATH:/opt/conda/bin
        echo "Installing Tools with apt-get "
        apt-get update
        apt-get install -y --no-install-recommends g++ make automake autoconf bzip2 unzip wget sox libtool git subversion python2.7 zlib1g-dev ca-certificates patch ffmpeg vim 
        cd /
        git clone https://github.com/kaldi-asr/kaldi.git
        cd kaldi/tools
        ./extras/install_mkl.sh
        make
        cd /kaldi/src
        ./configure --shared --use-cuda=no
        make depend
        make

%environment
        SHELL=/bin/bash
        export SHELL

