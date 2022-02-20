# Docker base image for debian 10-dbg

FROM marcelofpfelix/debian:10-se

ENV REFRESHED_AT 2022-02-12

# #############################################################################
# Arguments

ARG PACKAGES=" \
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
        wget \
        gnupg \
        "

WORKDIR /tmp

RUN set -o nounset -o errexit -o xtrace -o verbose && \
    # install packages
    apt-get install -y --no-install-recommends --no-install-suggests ${PACKAGES} && \
    apt-get clean

ARG GIT_COMMIT \
    GIT_COMMIT_DATE

ENV BASEIMAGE_GIT_COMMIT=$GIT_COMMIT \
    BASEIMAGE_GIT_COMMIT_DATE=$GIT_COMMIT_DATE \