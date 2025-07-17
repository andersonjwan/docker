# syntax=docker/dockerfile:1
FROM ubuntu:24.04

RUN apt-get update && \
    apt-get install --assume-yes curl libasound2t64 && \
    apt-get clean && \
    rm --recursive --force /var/lib/apt/lists/*

RUN curl --location --output /tmp/foxglove.deb "https://get.foxglove.dev/desktop/v2.31.2/foxglove-studio-2.31.2-linux-amd64.deb" && \
    apt-get update && \
    apt-get install --assume-yes /tmp/foxglove.deb && \
    rm --force /tmp/foxglove.deb

CMD ["/bin/foxglove-studio", "--no-sandbox"]
