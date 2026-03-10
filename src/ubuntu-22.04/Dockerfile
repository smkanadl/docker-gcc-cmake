# escape=`

FROM ghcr.io/smkanadl/ado-base-images:ubuntu-22.04-node-24

LABEL org.opencontainers.image.source="https://github.com/smkanadl/docker-gcc-cmake"

# https://apt.kitware.com/
# https://lindevs.com/install-vcpkg-on-ubuntu

ENV CMAKE_VERSION=3.31.5

RUN apt-get update && `
    DEBIAN_FRONTEND=noninteractive TZ=Europe/Berlin apt-get install -y `
    git `
    build-essential `
    gcc-11 `
    g++-11 `
    pkg-config `
    ca-certificates `
    gpg `
    wget `
    curl `
    zip `
    unzip `
    tar `
    mono-complete `
    && wget https://github.com/Kitware/CMake/releases/download/v$CMAKE_VERSION/cmake-$CMAKE_VERSION-linux-x86_64.sh -O /tmp/cmake.sh `
    && chmod +x /tmp/cmake.sh `
    && mkdir -p /opt/cmake-$CMAKE_VERSION `
    && /tmp/cmake.sh --skip-license --prefix=/opt/cmake-$CMAKE_VERSION `
    && ln -s /opt/cmake-$CMAKE_VERSION/bin/cmake /usr/local/bin/cmake `
    && ln -s /opt/cmake-$CMAKE_VERSION/bin/ctest /usr/local/bin/ctest `
    && ln -s /opt/cmake-$CMAKE_VERSION/bin/cpack /usr/local/bin/cpack `
    && rm -rf /tmp/cmake.sh `
	# smoke test
	&& cmake --version `
	&& ctest --version `
	&& cpack --version `
    && rm -rf /var/lib/apt/lists/* && `
    update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-11 40 && `
    update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-11 40 && `
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
