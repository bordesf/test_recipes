# This is a dockerfile that sets up a full Gym install with test dependencies
Bootstrap: docker

# Here we ll build our container upon the tensorflow container
From: tensorflow/tensorflow:latest-gpu-py3

# Then we put everything we need to install
%post
touch /toto.txt

%environment
SHELL=/bin/bash
export SHELL
