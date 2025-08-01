# Base image
ARG BUILD_FROM
FROM $BUILD_FROM

# Exit immediately if a command exits with a non-zero status
RUN set -e

# Update base image packages
RUN apt-get update \
  && apt-get upgrade -y \
  && rm -rf /var/lib/apt/lists/*

# Install base dependencies
RUN apt-get update \
  && apt-get install -y \
    apt-transport-https \
    curl \
    gpg \
    lsb-release \
    wget \
  && rm -rf /var/lib/apt/lists/*

# Install Hyperion
RUN curl -fsSL https://releases.hyperion-project.org/hyperion.pub.key | gpg --dearmor -o /usr/share/keyrings/hyperion.pub.gpg \
  && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hyperion.pub.gpg] https://apt.releases.hyperion-project.org/ $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/hyperion.list \
  && apt-get update \
  && apt-get install -y \
    hyperion=2.1.1* \
  && rm -rf /var/lib/apt/lists/*

# Copy root filesystem
COPY rootfs /

# Setup the config volume
VOLUME /config

# Expose the ports
EXPOSE 8090 8092 19333 19400 19444 19445
