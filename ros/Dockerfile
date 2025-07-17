# syntax=docker/dockerfile:1
FROM ubuntu:24.04

# Set up the locale.
#
# This localization setup is necessary to recreate the same environment that the
# ROS distribution is tested on, accordingly.
#
# For more information, see:
# https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debs.html#set-locale
RUN export DEBIAN_FRONTEND="noninteractive" && \
    apt-get update && \
    apt-get install --assume-yes locales && \
    locale-gen en_US en_US.UTF-8 && \
    update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8 && \
    apt-get clean && \
    rm --recursive --force /var/cache/apt/archives /var/lib/apt/lists/*

ENV LANG=en_US.UTF-8

# Enable the ROS repositories.
#
# This will validate that pre-requisite repositories are setup and configured
# appropriately before enabling the repositories for ROS.
RUN export DEBIAN_FRONTEND="noninteractive" && \
    apt-get update && \
    apt-get install --assume-yes software-properties-common && \
    add-apt-repository universe && \
    apt-get clean && \
    rm --recursive --force /var/cache/apt/archives /var/lib/apt/lists/*

RUN export DEBIAN_FRONTEND="noninteractive" && \
    apt-get update && \
    apt-get install --assume-yes curl && \
    apt-get clean && \
    rm --recursive --force /var/cache/apt/archives /var/lib/apt/lists/*

# Install the ROS configurations for APT.
#
# This will retrieve the latest ROS package for Ubuntu-based systems based on the
# version codename (e.g., "noble") and install it, accordingly.
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
    apt-get install --assume-yes ros-dev-tools && \
    apt-get install --assume-yes ros-jazzy-desktop && \
    apt-get clean && \
    rm --recursive --force /var/cache/apt/archives /var/lib/apt/lists/*
