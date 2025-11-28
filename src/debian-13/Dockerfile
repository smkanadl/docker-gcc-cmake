# escape=`

FROM ghcr.io/smkanadl/ado-base-images:debian-13

LABEL org.opencontainers.image.source="https://github.com/smkanadl/docker-gcc-cmake"

# https://apt.kitware.com/
# https://lindevs.com/install-vcpkg-on-ubuntu
# https://medium.com/@hackthebox/installing-mongodb-7-0-community-edition-on-debian-12-bookworm-a-comprehensive-guide-19906ddb47ad

RUN apt-get update && `
    DEBIAN_FRONTEND=noninteractive TZ=Europe/Berlin apt-get install -y `
    git `
    build-essential `
    gcc-14 `
    g++-14 `
    pkg-config `
    ca-certificates `
    gpg `
    wget `
    curl `
    zip `
    unzip `
    tar `
    mono-complete `
    cmake `
    && `
    rm -rf /var/lib/apt/lists/* && `
    update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-14 40 && `
    update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-14 40 && `
    git clone https://github.com/Microsoft/vcpkg.git && `
    cd vcpkg && `
    git checkout fba75d09065fcc76a25dcf386b1d00d33f5175af && `
    ./bootstrap-vcpkg.sh -disableMetrics && `
    cd .. && `
    chmod -R 777 vcpkg

ENV `
    # VCPKG root
    VCPKG_INSTALLATION_ROOT=/vcpkg `
	VCPKG_DISABLE_METRICS=1
