# syntax=docker/dockerfile:1

# renovate: datasource=docker depName=alpine
ARG ALPINE_VERSION=3.20.1

FROM alpine:${ALPINE_VERSION} AS base

FROM base AS build

# renovate: datasource=github-releases depName=errata-ai/vale
ARG VALE_VERSION=v3.5.0

# Set up architecture-specific variables
RUN ARCH=$(uname -m) && \
    if [ "$ARCH" = "aarch64" ]; then \
        export ARCH=arm64; \
    else \
        export ARCH=64-bit; \
    fi \
    && echo $ARCH > /tmp/ARCH

RUN apk add --no-cache wget tar libc6-compat libstdc++ libgcc libressl

# Install Vale
RUN export ARCH=$(cat /tmp/ARCH) \
    && cd /tmp \
    && wget -q https://github.com/errata-ai/vale/releases/download/${VALE_VERSION}/vale_${VALE_VERSION#v}_Linux_${ARCH}.tar.gz \
    && tar -xvzf vale_${VALE_VERSION#v}_Linux_${ARCH}.tar.gz vale -C /tmp \
    && mv /tmp/vale /usr/local/bin

RUN chmod +x /usr/local/bin/vale

FROM base AS final

# Install required libraries
RUN apk add --no-cache libc6-compat libstdc++ libgcc libressl

COPY --from=build /usr/local/bin/vale /usr/local/bin

# Clear and enable Alpine caching
RUN mkdir -p /var/cache/apk \
    && ln -s /var/cache/apk /etc/apk/cache \
    && rm -rf /var/cache/apk/*

USER root
