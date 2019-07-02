# Reference of the kind of base you want to use (e.g., docker, debootstrap, shub).
Bootstrap: docker
# Select the docker image you want to use (Here we choose tensorflow)
From: tensorflow/tensorflow:latest-gpu-py3

################# Section: Defining the system #################################
# Commands in the %post section are executed within the container.
% post
        apt-get update $$
        apt-get install -y cmake libcupti-dev libyaml-dev wget unzip &&
        apt-get clean &&
        pip install tqdm &&
        mkdir /dataset &&
        mkdir /tmp_log &&
        mkdir /final_log

# Environment variables that should be sourced at runtime.
%environment
        # use bash as default shell
        SHELL=/bin/bash
        export SHELL
