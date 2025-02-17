# escape=`

FROM ghcr.io/smkanadl/ado-base-images:alpine-3.21

LABEL org.opencontainers.image.source="https://github.com/smkanadl/docker-gcc-cmake"

# Use VCPKG_FORCE_SYSTEM_BINARIES to force vcpkg to use installed stuff - rather than trying to download glibc based stuff that does not work!
# https://github.com/Docker-Hub-frolvlad/docker-alpine-mono/blob/master/Dockerfile
RUN apk add --no-cache mono --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing && `
    apk add --no-cache --virtual=.build-dependencies ca-certificates && `
    cert-sync /etc/ssl/certs/ca-certificates.crt && `
    apk del .build-dependencies

RUN apk update && `
    apk add `
    git `
    bash `
    sudo `
    shadow `
    build-base `
    musl-dev `
    curl `
    g++ `
    gcc `
    libstdc++ `
    make `
    ninja `
    cmake `
    wget `
    curl `
    zip `
    unzip `
    tar `
    pkgconfig && `
	# IMPORTANT: Downlaod a copy of NuGet as VCPKG_FORCE_SYSTEM_BINARIES prohibits downloads and REMOVE the .exe - othewise it will not be found!
	curl -o /usr/local/bin/nuget https://dist.nuget.org/win-x86-commandline/v6.13.1/nuget.exe && `
    git clone https://github.com/Microsoft/vcpkg.git && `
    cd vcpkg && `
    git checkout fba75d09065fcc76a25dcf386b1d00d33f5175af && `
    ./bootstrap-vcpkg.sh -disableMetrics && `
    cd .. && `
    chmod -R 777 vcpkg

ENV `
    # VCPKG root
    VCPKG_INSTALLATION_ROOT=/vcpkg `
    VCPKG_FORCE_SYSTEM_BINARIES=1 `
	VCPKG_DISABLE_METRICS=1
