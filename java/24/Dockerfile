FROM        --platform=$TARGETOS/$TARGETARCH eclipse-temurin:24-jdk-noble

LABEL       author="Irochi" maintainer="me@irochi.moe"

LABEL       org.opencontainers.image.source="https://github.com/irochi-moe/Pterodactyl_yolks"
LABEL       org.opencontainers.image.licenses=MIT

RUN         apt update -y \
            && apt install -y lsof ca-certificates openssl git tar sqlite3 fontconfig tzdata iproute2 libfreetype6 tini zip unzip locales curl jq libstdc++6 webp \
            && apt clean

ENV         LC_ALL=en_US.UTF-8
ENV         LANG=en_US.UTF-8
ENV         LANGUAGE=en_US.UTF-8

RUN         useradd -m -d /home/container -s /bin/bash container
USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

STOPSIGNAL SIGINT

COPY        --chown=container:container ./../entrypoint.sh /entrypoint.sh
RUN         chmod +x /entrypoint.sh
ENTRYPOINT    ["/usr/bin/tini", "-g", "--"]
CMD         ["/entrypoint.sh"]
