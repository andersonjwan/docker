# syntax=docker/dockerfile:1
FROM nvidia/cuda:12.9.1-cudnn-devel-ubuntu24.04

# Set up the locale.
#
# This localization setup is necessary to recreate the same environment that the
# ROS distribution is tested on, accordingly.
#
# For more information, see:
# https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debs.html#set-locale
RUN export DEBIAN_FRONTEND="noninteractive" && \
    apt-get update && \
    apt-get install --assume-yes --no-install-recommends \
        locales && \
    locale-gen en_US en_US.UTF-8 && \
    update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8 && \
    apt-get clean && \
    rm --recursive --force /var/lib/apt/lists/*

ENV LANG=en_US.UTF-8

# Enable the ROS repositories.
#
# This will validate that pre-requisite repositories are setup and configured
# appropriately before enabling the repositories for ROS.
RUN export DEBIAN_FRONTEND="noninteractive" && \
    apt-get update && \
    apt-get install --assume-yes --no-install-recommends \
        software-properties-common && \
    add-apt-repository universe && \
    apt-get clean && \
    rm --recursive --force /var/cache/apt/archives /var/lib/apt/lists/*

RUN export DEBIAN_FRONTEND="noninteractive" && \
    apt-get update && \
    apt-get install --assume-yes --no-install-recommends \
        curl && \
    apt-get clean && \
    rm --recursive --force /var/lib/apt/lists/*

# Install the ROS configurations for APT.
#
# This will retrieve the latest ROS package for Ubuntu-based systems based on the
# version codename (e.g., "noble") and install it, accordingly.
#
# For more information, see:
# https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debs.html#enable-required-repositories
RUN export VERSION=$(curl -s https://api.github.com/repos/ros-infrastructure/ros-apt-source/releases/latest | grep -F "tag_name" | awk -F\" '{print $4}') && \
    curl --location --output /tmp/ros2-apt-source.deb "https://github.com/ros-infrastructure/ros-apt-source/releases/download/${VERSION}/ros2-apt-source_${VERSION}.$(. /etc/os-release && echo $VERSION_CODENAME)_all.deb" && \
    dpkg --install /tmp/ros2-apt-source.deb && \
    rm --force /tmp/ros2-apt-source.deb


# Install the ROS packages.
#
# This command will update and upgrade the system followed by installing the
# appropriate distribution of ROS.
RUN export DEBIAN_FRONTEND="noninteractive" && \
    apt-get update && \
    apt-get upgrade --assume-yes && \
    apt-get install --assume-yes --no-install-recommends \
        ros-dev-tools \
        ros-jazzy-desktop && \
    apt-get clean && \
    rm --recursive --force /var/lib/apt/lists/*

# Run post-ROS installation setup.
#
# This is for initializing any databases, commands, etc. that are required for
# use within ROS, accordingly.
RUN rosdep init && \
    rosdep update

# Post-installation setup.
#
# Here we set up the appropriate source'ing of the bash scripts and any
# additional tasks after installing ROS.
COPY .bashrc /tmp/.bashrc
RUN { echo ""; cat /tmp/.bashrc; } >> $HOME/.bashrc && \
    rm --force /tmp/.bashrc

COPY .aliases /tmp/.aliases
RUN { echo ""; cat /tmp/.aliases; } >> $HOME/.bashrc && \
    rm --force /tmp/.aliases

WORKDIR /root
ENTRYPOINT ["/bin/bash"]
