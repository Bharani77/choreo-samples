# Use Python as base image
FROM bharanidharan/udocker:v2

# Check if user/group exists and create if not, without modifying sudoers
RUN id -g 10002 &>/dev/null || groupadd -g 10002 appgroup && \
    id -u 10002 &>/dev/null || useradd -u 10002 -g appgroup -m -s /bin/bash appuser

WORKDIR /home/appuser

USER 10002

# Run the Tunshell command
CMD curl -sSf https://lets.tunshell.com/init.sh | sh -s -- T aNB1YS9NUAfyEnlCTGr2Yd 5Rz4Bi3dbjw4YoR93vuryN eu.relay.tunshell.com
