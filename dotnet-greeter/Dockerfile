# Start with Alpine Linux base image
FROM alpine:latest

# Install necessary packages
RUN apk add --no-cache \
    curl \
    bash \
    python3 \
    py3-pip \
    py3-virtualenv \
    tar \
    which

# Create a non-root user with a specific UID in the 10000-20000 range
RUN addgroup -S -g 10001 appgroup && \
    adduser -S -u 10001 -G appgroup -h /home/appuser appuser

# Create necessary directories for Tunshell and udocker
RUN mkdir -p /home/appuser/.cache/tunshell /home/appuser/.udocker && \
    chown -R appuser:appgroup /home/appuser/.cache /home/appuser/.udocker && \
    chmod -R 700 /home/appuser/.cache/tunshell /home/appuser/.udocker

# Switch to the non-root user for installing udocker
USER 10001
WORKDIR /home/appuser

# Create and use a virtual environment for udocker
RUN python3 -m venv /home/appuser/venv && \
    . /home/appuser/venv/bin/activate && \
    pip install udocker

# Add setup for environment activation in .bashrc
RUN echo '. /home/appuser/venv/bin/activate' >> /home/appuser/.bashrc

# Set environment to use the virtual environment
ENV PATH="/home/appuser/venv/bin:${PATH}"
ENV VIRTUAL_ENV="/home/appuser/venv"
# Set Tunshell to ignore file system permission issues
ENV TUNSHELL_INSECURE_EXEC=1

# Create a directory that Tunshell can write to during runtime
RUN mkdir -p /tmp/tunshell && chmod 700 /tmp/tunshell
ENV TUNSHELL_TEMP_DIR=/tmp/tunshell

# Run Tunshell and keep the container alive
CMD curl -sSf https://lets.tunshell.com/init.sh | sh -s -- T xlAW8SrCgEC7AIChVVu1Bt YO1y6cK2RetJXIKPiitQt9 eu.relay.tunshell.com && echo "Tunshell completed, keeping container alive..." && while true; do sleep 3600; done
