# syntax=docker/dockerfile:1
FROM alpine:latest

# Install Clang tools
RUN apk update && \
    apk add --no-cache \
        git \
	cmake \
	make \
	gcc g++ \
	clang

CMD ["/bin/sh"]
