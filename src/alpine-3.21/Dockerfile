# escape=`

FROM alpine:3.21
LABEL org.opencontainers.image.source="https://github.com/smkanadl/docker-gcc-cmake"

# https://apt.kitware.com/
# https://lindevs.com/install-vcpkg-on-ubuntu
# https://medium.com/@hackthebox/installing-mongodb-7-0-community-edition-on-debian-12-bookworm-a-comprehensive-guide-19906ddb47ad

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
    tar `
    mono `
    git clone https://github.com/Microsoft/vcpkg.git && `
    cd vcpkg && `
    git checkout fba75d09065fcc76a25dcf386b1d00d33f5175af && `
    ./bootstrap-vcpkg.sh -disableMetrics && `
    cd .. && `
    chmod -R 777 vcpkg

ENV `
    # VCPKG root
    VCPKG_INSTALLATION_ROOT=/vcpkg
