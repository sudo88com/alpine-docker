# syntax=docker/dockerfile:1

# renovate: datasource=docker depName=alpine
ARG ALPINE_VERSION=3.20.1

FROM alpine:${ALPINE_VERSION} AS base

FROM base AS final

# Install required libraries
RUN apk add --no-cache bash shellcheck

# Clear and enable Alpine caching
RUN mkdir -p /var/cache/apk \
    && ln -s /var/cache/apk /etc/apk/cache \
    && rm -rf /var/cache/apk/*

USER root
