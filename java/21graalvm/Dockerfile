FROM        --platform=$TARGETOS/$TARGETARCH container-registry.oracle.com/graalvm/jdk:21

LABEL       author="Irochi" maintainer="me@irochi.moe"

LABEL       org.opencontainers.image.source="https://github.com/irochi-moe/Pterodactyl_yolks"
LABEL       org.opencontainers.image.licenses=MIT

RUN         microdnf update \
            && microdnf install -y epel-release

RUN         microdnf update \
            && microdnf install -y curl lsof ca-certificates openssl git tar sqlite fontconfig tzdata iproute freetype tini zip unzip libstdc++ libwebp libwebp-devel libwebp-java libwebp-tools glibc-locale-source glibc-langpack-en \
            && microdnf clean all

ENV         LC_ALL=en_US.UTF-8
ENV         LANG=en_US.UTF-8
ENV         LANGUAGE=en_US.UTF-8

RUN         useradd -m -d /home/container -s /bin/bash container
USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

STOPSIGNAL SIGINT

COPY        --chown=container:container ./entrypoint.sh /entrypoint.sh
RUN         chmod +x /entrypoint.sh
ENTRYPOINT    ["/usr/bin/tini", "-g", "--"]
CMD         [ "/bin/bash", "/entrypoint.sh" ]
