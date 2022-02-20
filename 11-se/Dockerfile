# Docker base image for debian 11-se

FROM marcelofpfelix/debian:11

ENV REFRESHED_AT 2022-02-12

# #############################################################################
# Arguments
ARG S6_PATH=https://github.com/just-containers/s6-overlay/releases/download/v${S6_VERSION}/
ARG S6_FILE=s6-overlay-noarch-${S6_VERSION}.tar.xz
ARG S6_FILE2=s6-overlay-x86_64-${S6_VERSION}.tar.xz
ARG ENVTPL_PATH=https://github.com/mattrobenolt/envtpl/releases/download/$ENVTPL_VERSION/
ARG ENVTPL_FILE=envtpl-linux-amd64

ARG PACKAGES=" \
        ca-certificates \
        curl \
        xz-utils \
        "
WORKDIR /tmp
COPY files/SHA256SUMS .

RUN set -o nounset -o errexit -o xtrace -o verbose && \
    # install packages
    apt-get install -y --no-install-recommends --no-install-suggests ${PACKAGES} && \
    # s6 
    curl -sSL -O ${S6_PATH}${S6_FILE} && \
    tar -C / -Jxpf ${S6_FILE} && \
    curl -sSL -O ${S6_PATH}${S6_FILE2} && \
    tar -C / -Jxpf ${S6_FILE2} && \
    # envtpl
    curl -sSL ${ENVTPL_PATH}${ENVTPL_FILE} -o envtpl && \
    # sha256sum s6-overlay-* envtpl > SHA256SUMS
    sha256sum -c SHA256SUMS && \
    mv envtpl /bin && \
    chmod +x /bin/envtpl && \
    # cleaning
    rm ${S6_FILE} ${S6_FILE2} SHA256SUMS  && \
    apt-get autoremove --purge -y ${PACKAGES} && \
    apt-get clean

ARG GIT_COMMIT \
    GIT_COMMIT_DATE

ENV BASEIMAGE_GIT_COMMIT=$GIT_COMMIT \
    BASEIMAGE_GIT_COMMIT_DATE=$GIT_COMMIT_DATE \