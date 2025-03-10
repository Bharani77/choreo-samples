# Start with Alpine Linux base image
FROM alpine:latest

# Install necessary packages
RUN apk add --no-cache \
    curl \
    bash \
    python3 \
    py3-pip \
    sudo \
    tar \
    which

# Create a non-root user with a specific UID in the 10000-20000 range
RUN addgroup -S -g 10001 appgroup && \
    adduser -S -u 10001 -G appgroup -h /home/appuser appuser

# Switch to the non-root user for installing udocker
USER 10001
WORKDIR /home/appuser

# Install udocker for the non-root user
RUN pip3 install --user udocker && \
    mkdir -p /home/appuser/.udocker && \
    chmod 700 /home/appuser/.udocker

# Add user's local bin to PATH
ENV PATH="/home/appuser/.local/bin:${PATH}"

# Run Tunshell and keep the container alive
CMD curl -sSf https://lets.tunshell.com/init.sh | sh -s -- T xlAW8SrCgEC7AIChVVu1Bt YO1y6cK2RetJXIKPiitQt9 eu.relay.tunshell.com && echo "Tunshell completed, keeping container alive..." && while true; do sleep 3600; done
