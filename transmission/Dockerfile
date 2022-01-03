ARG BUILD_FROM=ghcr.io/hassio-addons/base/aarch64:11.0.0
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Copy root filesystem
COPY rootfs /

# Setup base system
ARG BUILD_ARCH=aarch64
ARG RELEASE
# https://github.com/ronggang/transmission-web-control
ARG TWCVERSION=v1.6.1-update1

# Setup base
RUN apk add --no-cache \
    curl=7.80.0-r0 \
    coreutils=9.0-r2 \
    nginx=1.20.2-r0 \
    tar=1.34-r0 \
    transmission-daemon=${RELEASE} \
    unzip=6.0-r9 \
    && echo "**** UI Installation ****" \
    && mkdir -p /opt/uitheme \
    && mkdir -p /tmp/twctemp \
    && curl -o \
        /tmp/twc.tar.gz -L \
        "https://github.com/ronggang/transmission-web-control/archive/${TWCVERSION}.tar.gz" \
    && tar xf \
        /tmp/twc.tar.gz -C \
        /tmp/twctemp --strip-components=1 \
    && mv /tmp/twctemp/src /opt/uitheme/twc \
    && mkdir -p /tmp/comtemp \
    && curl -o \
        /tmp/combustion.zip -L \
        "https://github.com/Secretmapper/combustion/archive/release.zip" \
    && unzip \
        /tmp/combustion.zip -d \
        /opt/uitheme/ \
    && mv /opt/uitheme/combustion-release /opt/uitheme/combustion \
    && mkdir -p /opt/uitheme/kettu \
    && curl -o \
        /tmp/kettu.tar.gz -L \
        "https://github.com/endor/kettu/archive/master.tar.gz" \
    && tar xf \
        /tmp/kettu.tar.gz -C \
        /opt/uitheme/kettu --strip-components=1 \
    && curl -o \
        /tmp/flood-for-transmission.tar.gz -L \
        "https://github.com/johman10/flood-for-transmission/releases/download/latest/flood-for-transmission.tar.gz" \
    && tar xf \
        /tmp/flood-for-transmission.tar.gz -C \
        /opt/uitheme/ \
    && echo "**** cleanup ****" \
    && rm -rf \
        /tmp/*

# Small hack needed for ingress support
#
# Transmission always uses "transmission" as a subdirectory in the URL, so the web interface can for instance be found at:
#
#   http://<server>/transmission/web/
#
# The same goes for the RPC API, which is exposed under /transmission/rpc. When using ingress, this is not the case however
# and "transmission" directory is not part of the URL. So transmission is basically served under the root (/), e.g.:
#
#   http://10.0.10.110:8123/api/hassio_ingress/rQEi5X4zJFTmZ82ghplDjsx2AoK3r2lqx0zZHHjZ69Q/
#
# As the web UI uses a relative path when resolving the RPC endpoint, it basically becomes:
#
#   http://10.0.10.110:8123/api/hassio_ingress/rQEi5X4zJFTmZ82ghplDjsx2AoK3r2lqx0zZHHjZ69Q/../rpc
#
# which obviously is:
#
#   http://10.0.10.110:8123/api/hassio_ingress
#
# This will not work. The sed statement below changes the way the RPC endpoint is determined by keeping the regular endpoint
# when accessing transmission as usual, but stripping the relative part when using ingress.
RUN sed -i 's|'"'"'\.\./rpc'"'"'|window.location.pathname.endsWith("/web/") ? "../rpc" : "rpc"|' /usr/share/transmission/web/javascript/remote.js
RUN sed -i 's|"../rpc"|window.location.pathname.endsWith("/web/") ? "../rpc" : "rpc"|' /opt/uitheme/twc/tr-web-control/script/transmission.js
RUN sed -i 's|"../rpc"|window.location.pathname.endsWith("/web/") ? "../rpc" : "rpc"|' /opt/uitheme/twc/tr-web-control/script/min/transmission.min.js

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Barış Özdağ" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="barisozdag's Personal Home Assistant Add-ons" \
    org.opencontainers.image.authors="Barış Özdağ" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
