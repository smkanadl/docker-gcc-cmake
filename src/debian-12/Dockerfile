# escape=`

FROM ghcr.io/smkanadl/ado-base-images:debian-12

LABEL org.opencontainers.image.source="https://github.com/smkanadl/docker-gcc-cmake"

# https://apt.kitware.com/
# https://lindevs.com/install-vcpkg-on-ubuntu
# https://medium.com/@hackthebox/installing-mongodb-7-0-community-edition-on-debian-12-bookworm-a-comprehensive-guide-19906ddb47ad

RUN apt-get update && `
    DEBIAN_FRONTEND=noninteractive TZ=Europe/Berlin apt-get install -y `
    git `
    build-essential `
    gcc-12 `
    g++-12 `
    pkg-config `
    ca-certificates `
    gpg `
    wget `
    curl `
    zip `
    unzip `
    tar `
    mono-complete `
    && `
    echo 'deb http://security.ubuntu.com/ubuntu focal-security main' | tee /etc/apt/sources.list.d/focal-security.list && `
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 871920D1991BC93C && `
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 3B4FE6ACC0B21F32 `
    && `
    wget -O - https://apt.kitware.com/keys/kitware-archive-latest.asc 2>/dev/null | gpg --dearmor - | tee /usr/share/keyrings/kitware-archive-keyring.gpg >/dev/null && `
    echo 'deb [signed-by=/usr/share/keyrings/kitware-archive-keyring.gpg] https://apt.kitware.com/ubuntu/ focal main' | tee /etc/apt/sources.list.d/kitware.list && `
    apt-get update && `
    rm /usr/share/keyrings/kitware-archive-keyring.gpg && `
    DEBIAN_FRONTEND=noninteractive TZ=Europe/Berlin apt-get install -y `
    kitware-archive-keyring `
    libssl1.1 `
    cmake `
    && `
    rm -rf /var/lib/apt/lists/* && `
    update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-12 40 && `
    update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-12 40 && `
    git clone https://github.com/Microsoft/vcpkg.git && `
    cd vcpkg && `
    git checkout fba75d09065fcc76a25dcf386b1d00d33f5175af && `
    ./bootstrap-vcpkg.sh -disableMetrics && `
    cd .. && `
    chmod -R 777 vcpkg

ENV `
    # VCPKG root
    VCPKG_INSTALLATION_ROOT=/vcpkg
