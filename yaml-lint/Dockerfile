# syntax=docker/dockerfile:1

# renovate: datasource=docker depName=alpine
ARG ALPINE_VERSION=3.20.1

FROM alpine:${ALPINE_VERSION} AS base

# renovate: datasource=pypi depName=yamllint
ARG YAMLLINT_VERSION=1.35.1

RUN apk add --no-cache python3 py3-pip

RUN python3 -m venv /venv \
    && . /venv/bin/activate \
    && pip install --no-cache-dir yamllint==${YAMLLINT_VERSION}

FROM alpine:${ALPINE_VERSION} AS final

RUN apk add --no-cache bash python3

# Copy the virtual environment from the build stage
COPY --from=base /venv /venv

# Ensure the virtual environment is activated
ENV PATH="/venv/bin:$PATH"

RUN yamllint --version

# Clear and enable Alpine caching
RUN mkdir -p /var/cache/apk \
    && ln -s /var/cache/apk /etc/apk/cache \
    && rm -rf /var/cache/apk/*

USER root

ENTRYPOINT ["bash", "-c"]
