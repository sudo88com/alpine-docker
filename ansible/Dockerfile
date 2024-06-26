# syntax=docker/dockerfile:1

# renovate: datasource=docker depName=alpine
ARG ALPINE_VERSION=3.20.1

FROM alpine:${ALPINE_VERSION} AS base

FROM base AS build

# renovate: datasource=pypi depName=ansible
ARG ANSIBLE_VERSION=10.1.0

# Set up architecture-specific variables
RUN ARCH=$(uname -m) && \
    if [ "$ARCH" = "aarch64" ]; then \
        export ARCH=arm64; \
    else \
        export ARCH=64bit; \
    fi \
    && echo $ARCH > /tmp/ARCH

RUN apk add --no-cache dpkg curl python3 py3-pip py3-virtualenv libffi-dev gcc musl-dev python3-dev

# Install Session Manager Plugin
RUN export ARCH=$(cat /tmp/ARCH) \
    && curl "https://s3.amazonaws.com/session-manager-downloads/plugin/latest/ubuntu_$ARCH/session-manager-plugin.deb" -o "session-manager-plugin.deb" \
    && dpkg -x session-manager-plugin.deb session-manager-plugin \
    && cp session-manager-plugin/usr/local/sessionmanagerplugin/bin/session-manager-plugin /usr/bin/session-manager-plugin \
    && chmod +x /usr/bin/session-manager-plugin

RUN python3 -m venv /venv \
    && . /venv/bin/activate \
    && pip install --no-cache-dir ansible==${ANSIBLE_VERSION} boto3

FROM base AS final

COPY --from=build /usr/bin/session-manager-plugin /usr/bin

RUN apk add --no-cache bash python3 openssh curl make aws-cli \
    && ln -s $(which aws) /bin/aws-cli

# Copy the virtual environment from the build stage
COPY --from=build /venv /venv

# Ensure the virtual environment is activated
ENV PATH="/venv/bin:$PATH"

RUN ansible --version

# Clear and enable Alpine caching
RUN mkdir -p /var/cache/apk \
    && ln -s /var/cache/apk /etc/apk/cache \
    && rm -rf /var/cache/apk/*

USER root
