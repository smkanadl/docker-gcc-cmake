# escape=`

FROM alpine:3.21
LABEL org.opencontainers.image.source="https://github.com/smkanadl/docker-gcc-cmake"

# https://github.com/Docker-Hub-frolvlad/docker-alpine-mono/blob/master/Dockerfile
RUN apk add --no-cache mono --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing && \
    apk add --no-cache --virtual=.build-dependencies ca-certificates && \
    cert-sync /etc/ssl/certs/ca-certificates.crt && \
    apk del .build-dependencies

RUN apk update && `
    apk add `
    git `
    bash `
    musl-dev `
    curl `
    g++ `
    make `
    cmake `
    wget `
    curl `
    zip `
    unzip `
    tar &&`
    git clone https://github.com/Microsoft/vcpkg.git && `
    cd vcpkg && `
    git checkout fba75d09065fcc76a25dcf386b1d00d33f5175af && `
    ./bootstrap-vcpkg.sh -disableMetrics && `
    cd .. && `
    chmod -R 777 vcpkg

ENV `
    # VCPKG root
    VCPKG_INSTALLATION_ROOT=/vcpkg
