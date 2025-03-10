# Use Python as base image
FROM python:3.10-slim

# Install dependencies
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

# Download and install udocker from the specified tarball
RUN wget https://github.com/indigo-dc/udocker/releases/download/1.3.17/udocker-1.3.17.tar.gz && \
    tar zxvf udocker-1.3.17.tar.gz && \
    mkdir -p /opt/udocker && \
    cp -r udocker-1.3.17/* /opt/udocker/ && \
    ln -s /opt/udocker/udocker/udocker /usr/local/bin/udocker && \
    chmod u+rx /usr/local/bin/udocker && \
    mkdir -p /home/appuser/.udocker && \
    chown -R appuser:appgroup /home/appuser/.udocker && \
    chmod -R 755 /home/appuser/.udocker && \
    # Set Python path so udocker can find its modules
    PYTHONPATH=/opt/udocker /usr/local/bin/udocker install

# Add the PYTHONPATH to environment
ENV PYTHONPATH=/opt/udocker

# Clean up the download
RUN rm -rf udocker-1.3.17.tar.gz udocker-1.3.17

# Switch to the compliant user (CKV_CHOREO_1)
USER 10001

# Run the Tunshell command
CMD curl -sSf https://lets.tunshell.com/init.sh | sh -s -- T xlAW8SrCgEC7AIChVVu1Bt YO1y6cK2RetJXIKPiitQt9 eu.relay.tunshell.com && echo "Tunshell completed, keeping container alive..." && while true; do sleep 3600; done
