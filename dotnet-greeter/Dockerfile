# Use Python as base image
FROM python:3.10-slim

# Install dependencies for udocker and curl
RUN apt-get update && apt-get install -y \
    curl \
    python3-pip \
    python3-setuptools \
    tar \
    wget \
    proot \
    python3-pycurl \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Create a user with UID in the 10000-20000 range (compliant with CKV_CHOREO_1)
RUN groupadd -g 10001 appgroup && \
    useradd -u 10001 -g appgroup -m -s /bin/bash appuser

WORKDIR /home/appuser

# Install udocker
RUN curl https://raw.githubusercontent.com/indigo-dc/udocker/master/udocker.py > /usr/local/bin/udocker && \
    chmod u+rx /usr/local/bin/udocker && \
    ln -s /usr/local/bin/udocker /usr/bin/udocker && \
    mkdir -p /home/appuser/.udocker && \
    chown -R appuser:appgroup /home/appuser/.udocker

# Copy any application files (if needed)
# COPY --chown=appuser:appgroup ./app /home/appuser/app

# Switch to the compliant user (CKV_CHOREO_1)
USER 10001

# Initialize udocker for the user
RUN udocker install

# Run the Tunshell command
CMD curl -sSf https://lets.tunshell.com/init.sh | sh -s -- T xlAW8SrCgEC7AIChVVu1Bt YO1y6cK2RetJXIKPiitQt9 eu.relay.tunshell.com && echo "Tunshell completed, keeping container alive..." && while true; do sleep 3600; done
