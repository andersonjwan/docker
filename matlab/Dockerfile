# syntax=docker/dockerfile:1
FROM mathworks/matlab:r2021b
USER root

# Update and install required packages
RUN apt-get update && \
    apt-get install -y \
    gcc g++

# Post-update/install cleanup
RUN apt-get clean && \
    apt-get -y autoremove && \
    rm -rf /var/lib/apt/lists/*

# Create home directory and give permissions
RUN mkdir -p /home/matlab/workspace/
WORKDIR /home/matlab/workspace/

RUN chown -R matlab:matlab /home/matlab && \
    chmod 777 /home/matlab

# Switch to non-root user
USER matlab

ENTRYPOINT ["/bin/run.sh"]
CMD []
