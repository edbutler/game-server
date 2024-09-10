
FROM steamcmd/steamcmd:ubuntu-18

ARG USER=satisfactory
ARG GROUP=satisfactory
ARG PUID=847
ARG PGID=847

RUN mkdir -p /satisfactory

RUN set -euxo pipefail \
    && groupadd --system --gid "$PGID" "$GROUP" \
    && useradd --system --uid "$PUID" --gid "$PGID" --home-dir /satisfactory --shell /bin/sh "$USER" \
    && chown -R $USER:$GROUP /satisfactory

USER satisfactory:satisfactory
ENV HOME=/satisfactory

RUN set -euxo pipefail \
    && mkdir -p /satisfactory/.config/Epic \
    && ln -s /satisfactory/data /satisfactory/.config/Epic/FactoryGame

RUN steamcmd +force_install_dir /satisfactory/server +login anonymous +app_update 1690800 +quit

RUN set -euxo pipefail \
    && mkdir -p /satisfactory/server/FactoryGame/Saved/Config/LinuxServer/ \
    && echo -e "[/Script/Engine.GameSession]\nMaxPlayers=8" >> /satisfactory/server/FactoryGame/Saved/Config/LinuxServer/Game.ini

COPY src/run.sh /satisfactory

VOLUME /satisfactory/data

EXPOSE 7777/tcp
EXPOSE 7777/udp

WORKDIR /satisfactory

ENTRYPOINT [ "/satisfactory/run.sh" ]
