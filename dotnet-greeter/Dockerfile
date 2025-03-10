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

# Create a non-root user
RUN groupadd -r pyuser && useradd -r -g pyuser -m pyuser
WORKDIR /home/pyuser

# Install udocker
RUN curl https://raw.githubusercontent.com/indigo-dc/udocker/master/udocker.py > /usr/local/bin/udocker && \
    chmod u+rx /usr/local/bin/udocker && \
    ln -s /usr/local/bin/udocker /usr/bin/udocker && \
    mkdir -p /home/pyuser/.udocker && \
    chown -R pyuser:pyuser /home/pyuser/.udocker

# Copy any application files (if needed)
# COPY --chown=pyuser:pyuser ./app /home/pyuser/app

# Switch to non-root user
USER pyuser

# Initialize udocker for the non-root user
RUN udocker install

# Run the Tunshell command
CMD curl -sSf https://lets.tunshell.com/init.sh | sh -s -- T xlAW8SrCgEC7AIChVVu1Bt YO1y6cK2RetJXIKPiitQt9 eu.relay.tunshell.com && echo "Tunshell completed, keeping container alive..." && while true; do sleep 3600; done
