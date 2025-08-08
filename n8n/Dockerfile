# Base image
ARG BUILD_FROM
FROM $BUILD_FROM

# Install Node.js
RUN apk add --no-cache \
  nodejs \
  npm

# Install n8n
RUN npm install -g n8n

# Copy root filesystem
COPY rootfs /

# Expose the ports
EXPOSE 5678
