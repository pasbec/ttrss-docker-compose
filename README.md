# ttrss-docker-compose

Docker Compose example setup for [Tiny Tiny RSS](https://tt-rss.org) with [LDAP authentication](https://github.com/pasbec/ttrss-auth-ldap.git) against some Active Directory domain controller.

## Setup

1. Create `.env` from `.env.example` to store secrets
1. Adjust at least all entries which are commented as "Mandatory" in `compose.yaml`
1. Bring the stack up in some local network, check the logs and test access
    ```sh
    docker compose up -d
    docker compose logs
    curl -ILfSs http://localhost/index.php
    ``` 
1. Protect your server wtih TLS or run it behind some proxy like [traefik](https://traefik.io/traefik/) before making it publicly available.

    > **Warning:**
    > Be aware that your (active directory) credentials are at risk if your server runs without encryption on some public network!

## Backup & Restore

```sh
docker compose run --rm --env ARCHIVE=backup.tar.gz backup
docker compose run --rm --env ARCHIVE=backup.tar.gz restore
```

## Upgrade

```sh
docker compose pull --ignore-buildable
docker compose build --pull
docker compose up -d
```