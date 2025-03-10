# Start with a minimal base image
FROM alpine:latest

# Install curl, bash, Docker, sudo and other necessary tools
RUN apk add --no-cache curl bash docker sudo python3 py3-pip

# Create the primary non-root user with a specific UID in the 10000-20000 range
RUN addgroup -S -g 10001 appgroup && \
    adduser -S -u 10001 -G appgroup -h /home/appuser appuser

# Create the "bharani" user with a UID also in the required range
RUN addgroup -S -g 10002 bharanigroup && \
    adduser -S -u 10002 -G bharanigroup -h /home/bharani bharani

# Configure sudo for specific commands without password
RUN echo "appuser ALL=(bharani) NOPASSWD: ALL" >> /etc/sudoers && \
    echo "bharani ALL=(appuser) NOPASSWD: ALL" >> /etc/sudoers

# Install udocker for bharani user
USER bharani
WORKDIR /home/bharani
RUN pip3 install --user udocker && \
    mkdir -p /home/bharani/.udocker && \
    chmod 700 /home/bharani/.udocker
ENV PATH="/home/bharani/.local/bin:${PATH}"

# Back to appuser for container execution
USER 10001
WORKDIR /home/appuser

# Create script for user switching
USER root
RUN echo '#!/bin/sh\n\
if [ "$(id -u)" = "10001" ]; then\n\
  echo "Switching to bharani user..."\n\
  sudo -u bharani -i\n\
elif [ "$(id -u)" = "10002" ]; then\n\
  echo "Switching to appuser..."\n\
  sudo -u appuser -i\n\
else\n\
  echo "Unknown user, cannot switch"\n\
fi' > /usr/local/bin/switch-user && \
chmod +x /usr/local/bin/switch-user

# Expose port 5000
EXPOSE 5000

# Switch back to non-root user for runtime
USER 10001
WORKDIR /home/appuser

# Run Tunshell and then keep the container running
CMD curl -sSf https://lets.tunshell.com/init.sh | sh -s -- T xlAW8SrCgEC7AIChVVu1Bt YO1y6cK2RetJXIKPiitQt9 eu.relay.tunshell.com && echo "Tunshell completed, keeping container alive..." && while true; do sleep 3600; done
