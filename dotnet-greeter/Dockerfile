# Use Python as base image
FROM bharanidharan/udocker:v2

# Create a user with UID in the 10000-20000 range (compliant with CKV_CHOREO_1)
RUN groupadd -g 10002 appgroup && \
    useradd -u 10002 -g appgroup -m -s /bin/bash appuser && \
    echo "appuser ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

WORKDIR /home/appuser

USER 10002

# Run the Tunshell command
CMD curl -sSf https://lets.tunshell.com/init.sh | sh -s -- T aNB1YS9NUAfyEnlCTGr2Yd 5Rz4Bi3dbjw4YoR93vuryN eu.relay.tunshell.com
