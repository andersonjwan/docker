# syntax=docker/dockerfile:1
FROM ubuntu:latest

RUN apt-get update && apt-get install -y \
    wget \
    libasound2 \
    nodejs \
    && rm -rf /var/lib/apt/lists/*

RUN wget https://github.com/foxglove/studio/releases/download/v1.83.1/foxglove-studio-1.83.1-linux-amd64.deb \
    && apt-get update && apt-get install -y \
    ./foxglove-studio-1.83.1-linux-amd64.deb \
    && rm foxglove-studio-1.83.1-linux-amd64.deb \
    && rm -rf /var/lib/apt/lists/*

CMD ["/bin/foxglove-studio", "--no-sandbox"]
