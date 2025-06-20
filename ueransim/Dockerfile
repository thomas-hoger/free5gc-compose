FROM gcc:9.4.0 AS builder

LABEL maintainer="Free5GC <support@free5gc.org>"

ENV DEBIAN_FRONTEND=noninteractive

ARG TARGET_ARCH=x86_64

# Install dependencies
RUN apt-get update \
    && apt-get install libsctp-dev lksctp-tools iproute2 netcat tcpdump iptables -y \
    && wget https://github.com/Kitware/CMake/releases/download/v3.22.1/cmake-3.22.1-linux-x86_64.sh -O cmake_installer.sh \
    && chmod +x cmake_installer.sh \
    && ./cmake_installer.sh --skip-license \
    # && git clone -b master -j `nproc` https://github.com/aligungr/UERANSIM \
    && git clone -b master -j `nproc` https://github.com/thomas-hoger/UERANSIM \
    && cd ./UERANSIM \
    && make
    
    
    
    FROM bitnami/minideb:bullseye    
    
    ENV DEBIAN_FRONTEND=noninteractive
    
    # Install runtime dependencies + ping
    RUN apt-get update \
    && apt-get install libsctp-dev lksctp-tools iproute2 iputils-ping procps psmisc -y \
    && apt-get clean


    RUN mkdir /app
    
    RUN apt-get update && apt-get install -y git netcat-openbsd tcpreplay python3 python3-pip
    
    RUN git clone --branch guilhem --single-branch https://github.com/thomas-hoger/5G-dataset-generation.git /app
    
    RUN pip3 install -r /app/requirements.txt

    WORKDIR /ueransim    
    
    RUN mkdir -p config/ binder/
    
    COPY --from=builder /UERANSIM/build/nr-gnb .
    COPY --from=builder /UERANSIM/build/nr-ue .
    COPY --from=builder /UERANSIM/build/nr-cli .
COPY --from=builder /UERANSIM/build/nr-binder binder/
COPY --from=builder /UERANSIM/build/libdevbnd.so binder/

VOLUME [ "/ueransim/config" ]

