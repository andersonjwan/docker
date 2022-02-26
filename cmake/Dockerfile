# syntax=docker/dockerfile:1
FROM debian:11

# Install `build-essential` tools
RUN apt-get update
RUN apt-get -y install \
    build-essential \
    libssl-dev \
    wget

# Remove any older versions of `cmake`
RUN apt-get remove --purge cmake && \
    hash -r

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
