# syntax=docker/dockerfile:1
FROM ubuntu:22.04

RUN apt-get update && apt-get install -y \
    wget \
    libasound2 \
    nodejs \
    && rm -rf /var/lib/apt/lists/*

RUN wget https://get.foxglove.dev/desktop/latest/foxglove-studio-2.7.0-linux-amd64.deb \
    && apt-get update && apt-get install -y \
    ./foxglove-studio-2.7.0-linux-amd64.deb \
    && rm foxglove-studio-2.7.0-linux-amd64.deb \
    && rm -rf /var/lib/apt/lists/*

CMD ["/bin/foxglove-studio", "--no-sandbox"]
