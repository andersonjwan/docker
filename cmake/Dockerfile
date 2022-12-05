# syntax=docker/dockerfile:1
FROM alpine:latest

# Install `build-essential` tools
RUN apk update && \
    apk add --no-cache \
        linux-headers \
        make \
        automake \
        gcc g++ \
        openssl-dev \
        wget

# Remove any older versions of `cmake`
RUN apk del cmake

# Download CMake source files
RUN wget https://github.com/Kitware/CMake/releases/download/v3.25.1/cmake-3.25.1.tar.gz

# Extract source files
RUN tar -zxvf cmake-3.25.1.tar.gz

# Compile CMake source files
WORKDIR cmake-3.25.1/
RUN chmod +x bootstrap && \
    ./bootstrap
RUN make && make install

WORKDIR /home/
RUN rm -rf /cmake-3.25.1/ /cmake-3.25.1.tar.gz

CMD ["/bin/sh"]
