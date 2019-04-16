# This is a dockerfile that sets up a full Gym install with test dependencies
Bootstrap: docker

# Here we ll build our container upon the tensorflow container
From: tensorflow/tensorflow:latest-gpu-py3

# Then we put everything we need to install
%post
apt -y update && \
apt install -y keyboard-configuration && \
apt install -y \
python3-setuptools \
python3-dev \
python-pyglet \
python3-opengl \
libjpeg-dev \
libboost-all-dev \
libsdl2-dev \
libosmesa6-dev \
patchelf \
ffmpeg \
xvfb \
wget \
git \
unzip && \
apt clean && \
rm -rf /var/lib/apt/lists/*

# Download Gym and Mujoco
mkdir /Gym && cd /Gym
git clone https://github.com/openai/gym.git || true && \
mkdir /Gym/.mujoco && cd /Gym/.mujoco
wget https://www.roboti.us/download/mjpro150_linux.zip  && \
unzip mjpro150_linux.zip && \
wget https://www.roboti.us/download/mujoco200_linux.zip && \
unzip mujoco200_linux.zip && \
mv mujoco200_linux mujoco200

# Export global environment variables
export MUJOCO_KEY='replacebyyourkey'
export MUJOCO_PY_MJKEY_PATH=/Gym/.mujoco/mjkey.txt
export MUJOCO_PY_MUJOCO_PATH=/Gym/.mujoco/mujoco200/
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/Gym/.mujoco/mjpro150/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/Gym/.mujoco/mujoco200/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/bin
echo $MUJOCO_KEY | base64 --decode > /Gym/.mujoco/mjkey.txt

# Install python dependencies
wget https://raw.githubusercontent.com/openai/mujoco-py/master/requirements.txt
pip install -r requirements.txt
# Install everything
cd /Gym/gym
pip install -e '.[all]'
# Change permission to use mujoco_py as non sudoer user
chmod -R 777 /usr/local/lib/python3.5/dist-packages/mujoco_py/

# Export global environment variables
%environment
export SHELL=/bin/bash
export MUJOCO_KEY='replacebyyourkey'
export MUJOCO_PY_MJKEY_PATH=/Gym/.mujoco/mjkey.txt
export MUJOCO_PY_MUJOCO_PATH=/Gym/.mujoco/mujoco200/
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/Gym/.mujoco/mjpro150/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/Gym/.mujoco/mujoco200/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/bin
export PATH=/Gym/gym/.tox/py3/bin:$PATH

%runscript
exec /bin/bash "$@"
