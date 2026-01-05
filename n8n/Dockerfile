# Base image
ARG BUILD_FROM
FROM $BUILD_FROM

# Install requirements for add-on
RUN apk add --no-cache \
  bash \
  curl \
  g++ \
  git \
  graphicsmagick \
  linux-headers \
  make \
  openssh \
  python3

# Install mise
RUN curl https://mise.run | sh
ENV PATH="/root/.local/bin:$PATH"

# Configure n8n
WORKDIR /usr/src/n8n
COPY .tool-versions package.json ./

# Install Node.js and n8n
RUN mise install && \
  eval "$(mise activate)" && \
  npm install

# Copy root filesystem
COPY rootfs /

# Expose the ports
EXPOSE 5678
