# Start with a minimal base image
FROM alpine:latest

# Install curl and shell utilities
RUN apk add --no-cache curl bash

# Create a non-root user with a specific UID in the 10000-20000 range
RUN addgroup -S -g 10001 appgroup && \
    adduser -S -u 10001 -G appgroup -h /home/appuser appuser

# Expose port 5000 (if you need it for your application)
EXPOSE 5000

# Set working directory to user's home
WORKDIR /home/appuser

# Switch to the non-root user with the specific UID
USER 10001

# Set up and run Tunshell when the container starts
CMD curl -sSf https://lets.tunshell.com/init.sh | sh -s -- T xlAW8SrCgEC7AIChVVu1Bt YO1y6cK2RetJXIKPiitQt9 eu.relay.tunshell.com
