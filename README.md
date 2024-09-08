# Game Server

## Prerequisites

Assumes games are being run in a virtual machine with:
- A data drive mounted at `/data` where game data will be persisted
- The `docker` command (see https://docs.docker.com/engine/install/ubuntu/)

## Updating Games

Since all these dockerfiles pull the games from the internet, you'll need to rebuild them without the cache to update the game servers.
