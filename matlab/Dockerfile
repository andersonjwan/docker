ARG MATLAB_RELEASE=r2022a
FROM mathworks/matlab-deps:${MATLAB_RELEASE}

ARG MATLAB_RELEASE

# Install packages.
# This includes package dependencies for MPM and MEX-based support
# for Mathworks.
RUN export DEBIAN_FRONTEND=noninteractive && apt-get update && \
    apt-get install --no-install-recommends --yes \
        gcc g++ \
        git-svn \
        wget \
        unzip \
        ca-certificates && \
    apt-get clean && apt-get autoremove

# Install MATLAB products.
# Using MPM, the set of MATLAB products are defined from the --products flag.
RUN wget -q https://www.mathworks.com/mpm/glnxa64/mpm && \
    chmod +x mpm && \
    ./mpm install \
        --release=${MATLAB_RELEASE} \
        --destination=/opt/matlab \
        --products MATLAB Simulink && \
    rm -f mpm /tmp/mathworks_root.log && \
    ln -s /opt/matlab/bin/matlab /usr/local/bin/matlab

# Create a MATLAB user.
# The default $USER name of the OS.
RUN adduser --shell /bin/bash --disabled-password --gecos "" matlab && \
    echo "matlab ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/matlab && \
    chmod 0440 /etc/sudoers.d/matlab

# Mathworks Docker usage reporting options.
# Disabled by default. Set MW_DDUX_FORCE_ENABLE to true to send diagnostics
# and usage reports.
ENV MW_DDUX_FORCE_ENABLE=false MW_CONTEXT_TAGS=MATLAB:DOCKERFILE:V1

# Setup instance.
USER matlab
WORKDIR /home/matlab/
ENTRYPOINT ["matlab"]
