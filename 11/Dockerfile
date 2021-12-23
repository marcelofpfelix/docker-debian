# Docker base image for debian 11

FROM debian:11.1-slim

ENV REFRESHED_AT 2021-12-01

RUN set -o nounset -o errexit -o xtrace -o verbose && \
    apt-get update -qq && \
    apt-get upgrade && \
    apt-get install -y --no-install-recommends --no-install-suggests \
        ca-certificates \
        curl \
        dnsutils \
        inotify-tools \
        iproute2 \
        iputils-ping \
        jq \
        mtr-tiny \
        netcat \
        openssl \
        procps \
        socat \
        traceroute \
        vim-tiny \
        wget && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

