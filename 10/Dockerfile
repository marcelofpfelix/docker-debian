# Docker base image for debian 10

FROM debian:10-slim

ENV REFRESHED_AT 2022-02-12

# #############################################################################
# Arguments
ARG OS_VERSION=buster
ARG FRR_VERSION=8
ARG KAMAILIO_VERSION=5.5.2
ARG S6_VERSION=1.19.1.1
ARG ENVTPL_VERSION=0.2.0

ARG PACKAGES=" \
        ca-certificates \
        curl \
        gnupg \
        "

# #############################################################################
# apt setup
RUN set -o nounset -o errexit -o xtrace -o verbose && \
    # update packages
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends --no-install-suggests ${PACKAGES} && \
    # add frr repo
    curl -s https://deb.frrouting.org/frr/keys.asc | apt-key add - && \
    echo deb https://deb.frrouting.org/frr ${OS_VERSION} frr-${FRR_VERSION} | tee -a /etc/apt/sources.list.d/frr.list && \
    # add kamailio repo
    curl -s https://deb-archive.kamailio.org/kamailiodebkey.gpg | apt-key add - && \
    echo deb https://deb-archive.kamailio.org/repos/kamailio-${KAMAILIO_VERSION} ${OS_VERSION} main | tee -a /etc/apt/sources.list.d/frr.list && \
    apt-get update && \
    apt-get autoremove --purge -y ${PACKAGES} && \
    apt-get clean

ARG GIT_COMMIT \
    GIT_COMMIT_DATE

ENV BASEIMAGE_GIT_COMMIT=$GIT_COMMIT \
    BASEIMAGE_GIT_COMMIT_DATE=$GIT_COMMIT_DATE \
    # add versions to be used
    S6_VERSION=$S6_VERSION \
    ENVTPL_VERSION=$ENVTPL_VERSION