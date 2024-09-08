
FROM steamcmd/steamcmd:ubuntu-24

ARG USER=satisfactory
ARG GROUP=satisfactory
ARG PUID=847
ARG PGID=847

RUN mkdir -p /satisfactory

RUN set -euxo pipefail \
    && mkdir -p /satisfactory/.config/Epic/FactoryGame \
    && ln -s /satisfactory/data

RUN set -euxo pipefail \
    && groupadd --system --gid "$PGID" "$GROUP" \
    && useradd --system --uid "$PUID" --gid "$PGID" --home-dir /satisfactory --shell /bin/sh "$USER" \
    && chown -R $USER:$GROUP /satisfactory

RUN steamcmd +force_install_dir /satisfactory/server +login anonymous +app_update 1690800 +quit

# this is janky af but chowning the entire directory doubles the size of the image if cached...
RUN set -euxo pipefail \
    && mkdir -p /satisfactory/server/FactoryGame/Saved \
    && mkdir -p /satisfactory/server/Engine/Saved \
    && mkdir -p /satisfactory/server/FactoryGame/Intermediate \
    && chown $USER:$GROUP /satisfactory/server /satisfactory/server/FactoryGame/Saved /satisfactory/server/Engine/Saved /satisfactory/server/FactoryGame/Intermediate

COPY src/run.sh /satisfactory

VOLUME /satisfactory/data

USER satisfactory:satisfactory
ENV HOME=/satisfactory

EXPOSE 15777/udp
EXPOSE 15000/udp
EXPOSE 7777/udp

WORKDIR /satisfactory

ENTRYPOINT [ "/satisfactory/run.sh" ]
