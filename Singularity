Bootstrap: docker
FROM: pytorch/pytorch:1.0.1-cuda10.0-cudnn7-runtime
# Debian Stretch without manpages and other files
# usually not needed in containers.

%help

Contains R version 3.6.0

%post

# Packages needed inside the container.
export CONTAINER_SOFTWARE="gfortran g++ gcc make libcurl4-gnutls-dev"
## Set build variables.
# Packages needed only for the build process.
export BUILD_SOFTWARE="wget zlib1g-dev libbz2-dev liblzma-dev libpcre3-dev libcurl4-gnutls-dev"
# Needed for downloading source.
export R_BASE_URI="https://cran.r-project.org/src/base/R-3/"
export R_FOLDER_NAME="R-3.6.0"
export R_PACKAGE_NAME="${R_FOLDER_NAME}.tar.gz"
# Set paths to facilitate the build process.
export BUILDHOME="/tmp"

# Install build and run requirements.
apt-get update
apt-get install $BUILD_SOFTWARE $CONTAINER_SOFTWARE -y

# Get R Package
wget ${R_BASE_URI}${R_PACKAGE_NAME}
tar -xf $R_PACKAGE_NAME

# Build R
cd $R_FOLDER_NAME
./configure --with-readline=no --with-x=no --disable-java
make
make install

# Removing installation overhead.

cd
rm -rf /tmp/*
apt-get purge $BUILD_SOFTWARE -y
apt-get autoclean -y
apt-get autoremove -y
rm -rf /var/lib/apt/lists/*

%test

# Can we call R?
R --version
