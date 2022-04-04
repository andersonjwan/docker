# syntax=docker/dockerfile:1
FROM fedora:34

# Install `build-essential` tools
RUN dnf -y update
RUN dnf -y install \
    make automake gcc g++ openssl-devel wget

# Remove any older versions of `cmake`
RUN dnf -y remove cmake

# Download CMake source files
RUN wget https://github.com/Kitware/CMake/releases/download/v3.22.1/cmake-3.22.1.tar.gz

# Extract source files
RUN tar -zxvf cmake-3.22.1.tar.gz

# Compile CMake source files
WORKDIR cmake-3.22.1/
RUN chmod +x bootstrap && \
    ./bootstrap
RUN make && make install

CMD ["/bin/bash"]
