# escape=`

FROM ubuntu:18.04
LABEL org.opencontainers.image.source="https://github.com/smkanadl/docker-gcc-cmake"

# https://apt.kitware.com/
# https://www.mono-project.com/download/stable/#download-lin
# https://github.com/mono/mono/issues/21584
# https://lindevs.com/install-vcpkg-on-ubuntu

RUN apt-get update && `
    DEBIAN_FRONTEND=noninteractive TZ=Europe/Berlin apt-get install -y `
    git `
    build-essential `
    gcc-8 `
    g++-8 `
    pkg-config `
    ca-certificates `
    gpg `
    wget `
    curl `
    zip `
    unzip `
    tar `
    && `
    wget -O - https://apt.kitware.com/keys/kitware-archive-latest.asc 2>/dev/null | gpg --dearmor - | tee /usr/share/keyrings/kitware-archive-keyring.gpg >/dev/null && `
    echo 'deb [signed-by=/usr/share/keyrings/kitware-archive-keyring.gpg] https://apt.kitware.com/ubuntu/ bionic main' | tee /etc/apt/sources.list.d/kitware.list && `
    apt-get update && `
    rm /usr/share/keyrings/kitware-archive-keyring.gpg && `
    gpg --keyserver keyserver.ubuntu.com --recv 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF && `
    gpg --export 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF | tee /usr/share/keyrings/mono.gpg >/dev/null && `
    gpg --batch --yes --delete-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF && `
    echo 'deb [signed-by=/usr/share/keyrings/mono.gpg] https://download.mono-project.com/repo/ubuntu stable-bionic main' | tee /etc/apt/sources.list.d/mono-official-stable.list && `
    apt-get update && `
    DEBIAN_FRONTEND=noninteractive TZ=Europe/Berlin apt-get install -y `
    kitware-archive-keyring `
    cmake `
    mono-complete `
    && `
    rm -rf /var/lib/apt/lists/* && `
    update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 40 && `
    update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-8 40 && `
    git clone https://github.com/Microsoft/vcpkg.git && `
    cd vcpkg && `
    git checkout 501db0f17ef6df184fcdbfbe0f87cde2313b6ab1 && `
    ./bootstrap-vcpkg.sh -disableMetrics && `
    cd .. && `
    chmod -R 777 vcpkg

ENV `
    # VCPKG root
    VCPKG_INSTALLATION_ROOT=/vcpkg
