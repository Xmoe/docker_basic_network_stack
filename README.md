# Basic Network Stack using Docker

This stack enables you to quickly bring other containers online and expose them to the web using via https by setting just three environment variables.

To do this, this compose file sets up an nginx reverse-proxy and a certbot integration using [nginx-proxy](https://github.com/nginx-proxy/nginx-proxy) and [acme-companion](https://github.com/nginx-proxy/acme-companion), as well as a [portainer-ce](https://github.com/portainer/portainer) instance for management.

For further information, please check out the links above

## Running the stack

### Setting environment variables

You need to specify following environment variables to bring the stack online:

`LETSENCRYPT_EMAIL`

`PORTAINER_URL`

These can be set in the `.env` file. For example:

```
LETSENCRYPT_EMAIL=john.doe@example.com
PORTAINER_URL=portainer.example.com
```

### Starting the stack

Navigate into the directory containing the `docker-compose.yaml` and run

```
docker compose up -d
```

## Bringing other services online

Connecting other containers to the web using this stack is as simple as setting following environment variables for that container:

`VIRTUAL_HOST` - specifies the URL for that container

`VIRTUAL_PORT` - specifies the port of the container to which the URL will be bound (per default `80` is used)

`LETSECNRYPT_HOST` - specifies the URL for that container via HTTPS (typically the same as `VIRTUAL_HOST`)

For example:

```
VIRTUAL_HOST=wiki.example.com
VIRTUAL_PORT=8080
LETSENCRYPT_HOST=wiki.example.com
```

Do note, that this stack uses a network called `net`. All other containers that are to be exposed using this stack need to be in the network `net` as well.