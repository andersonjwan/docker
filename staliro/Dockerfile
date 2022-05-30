FROM andersonjwan/matlab:r2022a

# Install packages.
# The set of packages are dependencies need to run the Monitor Survey
# tool and tests.
RUN export DEBIAN_FRONTEND=noninteractive && sudo apt-get update && \
    sudo apt-get install --no-install-recommends --yes \
        python3 \
        python3-pip && \
    sudo apt-get clean && sudo apt-get autoremove

# Install Poetry
RUN pip install --user poetry

# Create user.
# The default $USER name of the system.
# RUN adduser --shell /bin/bash --disabled-password --gecos "" monsurvey && \
#     echo "monsurvey ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/monsurvey && \
#     chmod 0440 /etc/sudoers.d/monsurvey

# Setup MATLAB licensing.
# There are two options: (1) copy license file to container (default),
# or (2) point to a network license manager.
ARG LICENSE
RUN if [[ -z "${LICENSE}"]]; \
    then echo "Please provide a MATLAB license file." && exit; \
    else echo "MATLAB license provided. Thanks!"; fi
ENV MLM_LICENSE_FILE=/opt/matlab/licenses/${LICENSE}

# Comment the next line if network license manager is used instead of copying
# a license file.
COPY ${LICENSE} /opt/matlab/licenses/

# Install S-TaLiRo
WORKDIR /home/matlab/
RUN git svn clone https://subversion.assembla.com/svn/s-taliro_public/trunk/dp_taliro && \
    git svn clone https://subversion.assembla.com/svn/s-taliro_public/trunk/tp_taliro

RUN cd /home/matlab/dp_taliro/ && matlab -batch setup_dp_taliro && \
    cd /home/matlab/tp_taliro/ && matlab -batch setup_tp_taliro

# Setup entrypoint.
WORKDIR /home/matlab/
ENTRYPOINT ["/bin/bash"]
