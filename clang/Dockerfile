# syntax=docker/dockerfile:1
FROM alpine:latest

# Install Clang tools
RUN apk update && \
    apk add --no-cache \
        clang-extra-tools

CMD ["/bin/sh"]
