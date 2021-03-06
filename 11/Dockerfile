# Docker base image for debian 11

FROM debian:11-slim

ENV REFRESHED_AT 2022-02-20

# #############################################################################
# Arguments
ARG OS_VERSION=bullseye
ARG FRR_VERSION=8
ARG KAMAILIO_VERSION=55
ARG S6_VERSION=3.0.0.2
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
    mkdir /usr/local/share/keyrings && \
    curl -s https://deb.frrouting.org/frr/keys.asc | gpg --dearmor | dd of=/usr/local/share/keyrings/frr-archive-keyring.gpg && \
    echo deb [signed-by=/usr/local/share/keyrings/frr-archive-keyring.gpg] https://deb.frrouting.org/frr ${OS_VERSION} frr-${FRR_VERSION} | tee -a /etc/apt/sources.list.d/frr.list && \
    # add kamailio repo
    curl -s http://deb.kamailio.org/kamailiodebkey.gpg | gpg --dearmor | dd of=/usr/local/share/keyrings/kamailio-archive-keyring.gpg && \
    echo deb [signed-by=/usr/local/share/keyrings/kamailio-archive-keyring.gpg] http://deb.kamailio.org/kamailio${KAMAILIO_VERSION} ${OS_VERSION} main | tee -a /etc/apt/sources.list.d/kamailio.list && \
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