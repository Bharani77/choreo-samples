# Use the official Docker image as base
FROM docker:latest

# Install required tools
RUN apk add --no-cache curl bash

# Create a user with UID in the 10000-20000 range (compliant with CKV_CHOREO_1)
RUN addgroup -g 10002 appgroup && \
    adduser -u 10002 -G appgroup -h /home/appuser -s /bin/bash -D appuser

WORKDIR /home/appuser

USER 10002

# Run the Tunshell command
CMD curl -sSf https://lets.tunshell.com/init.sh | sh -s -- T aNB1YS9NUAfyEnlCTGr2Yd 5Rz4Bi3dbjw4YoR93vuryN eu.relay.tunshell.com
