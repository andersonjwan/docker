# syntax=docker/dockerfile:1
FROM andersonjwan/devel:latest

# Install Clang tools
RUN apk update && \
    apk add --no-cache \
        clang-extra-tools

CMD ["/bin/sh"]
