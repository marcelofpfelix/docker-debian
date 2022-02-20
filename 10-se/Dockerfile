# Docker base image for debian 10-se

FROM marcelofpfelix/debian:10

ENV REFRESHED_AT 2022-02-12

# #############################################################################
# Arguments
ARG S6_PATH=https://github.com/just-containers/s6-overlay/releases/download/v${S6_VERSION}/
ARG S6_FILE=s6-overlay-amd64.tar.gz
ARG ENVTPL_PATH=https://github.com/mattrobenolt/envtpl/releases/download/$ENVTPL_VERSION/
ARG ENVTPL_FILE=envtpl-linux-amd64

ARG PACKAGES=" \
        ca-certificates \
        curl \
        "
WORKDIR /tmp
COPY files/SHA256SUMS .

RUN set -o nounset -o errexit -o xtrace -o verbose && \
    # install packages
    apt-get install -y --no-install-recommends --no-install-suggests ${PACKAGES} && \
    # s6 
    curl -sSL -O ${S6_PATH}${S6_FILE} && \
    tar zxf ${S6_FILE} -C / && \
    # envtpl
    curl -sSL ${ENVTPL_PATH}${ENVTPL_FILE} -o envtpl && \
    # sha256sum s6-overlay-amd64.tar.gz envtpl > SHA256SUMS
    sha256sum -c SHA256SUMS && \
    mv envtpl /bin && \
    chmod +x /bin/envtpl && \
    # cleaning
    rm ${S6_FILE} SHA256SUMS  && \
    apt-get autoremove --purge -y ${PACKAGES} && \
    apt-get clean

ARG GIT_COMMIT \
    GIT_COMMIT_DATE

ENV BASEIMAGE_GIT_COMMIT=$GIT_COMMIT \
    BASEIMAGE_GIT_COMMIT_DATE=$GIT_COMMIT_DATE \