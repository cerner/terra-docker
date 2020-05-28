# terra-node-dev

This dockerfile provides a docker image setup with zshell for developers to use as a common node development environment. This image copies no code in and can be used directly with a volume mount to add code to the /opt/module directory.

## API (of a sort)

* Zsh terminal
* History caching location: `/root/zsh_history/`

## Usage

This docker container provides a zsh instance to develop in using the same version of npm and node as our CI system, effectively providing a consistent development environment for terra development. It's best used with docker compose. An example follows:

```yml
version: '3'

services:
  dev:
    image: cerner/terra-node-dev:1
    ports:
      - 8080:8080
    volumes:
      - .:/opt/module
      - zsh_history:/root/zsh_history

volumes:
  zsh_history:

```

This docker compose file sets up the dev docker container. It pulls a global image. Maps the port 8080 to the host's port 8080. Volume mounts the repo into the module folder to provide code to work and develop against. This also has the added benefit of caching node modules between runs of the docker container. Finally it uses a docker volume to cache the shell history between docker runs as well.

To develop use the following command. The `--service-ports` flag is required otherwise the 8080 port won't be mapped. This will spin up a zsh instance with your code mounted to it.

```bash
dc run --service-ports dev
```

### Upsides

* isolated dev env
* cross os compatibility
* quick setup

### Downsides

* Docker compose files are not re-useable.
  * You'll find yourself duplicating these files in each project you work in.
* Only one dev env can bind to 8080 on the host.
  * You can either change the port manually or only run one container server at a time.
* slower.

### Named module directory

By default the directory the repo gets mounted into is called `module`. This can be customized by extending the dev docker container and docker-compose file as follows:

#### dev.dockerfile

```dockerfile
# use node as base image
FROM cerner/terra-node-dev:1

WORKDIR /opt/test
```

```yml
version: '3'

services:
  dev:
    build:
      context: .
      dockerfile: dev.dockerfile
    ports:
      - 8080:8080
    volumes:
      - .:/opt/test
      - zsh_history:/root/zsh_history

volumes:
  zsh_history:

```
