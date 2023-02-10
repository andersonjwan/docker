# syntax=docker/dockerfile:1
FROM andersonjwan/cmake:latest

# Install Clang tools
RUN apk update && \
    apk add --no-cache \
        git \
        clang \
        curl \
        openjdk17 \
        python3 \
        clang-extra-tools

# Install ANTLR tool
RUN curl -L -O https://raw.githubusercontent.com/antlr/website-antlr4/gh-pages/download/antlr-4.11.1-complete.jar --output-dir /usr/local/bin && \
    chmod +x /usr/local/bin/antlr-4.11.1-complete.jar

CMD ["/bin/sh"]
