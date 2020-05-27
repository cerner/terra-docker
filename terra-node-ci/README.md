# terra-node-ci

This dockerfile provides a docker image for terra projects to extend to use in CI it will copy code as well as run npm install by default.

## API (of a sort)

* Extends terra-node-base
* On build: Copies . to /opt/module
* On build: Runs Npm Install

## Usage

This docker container is expected to be extended by a project specific docker container, see example below.

```dockerfile
# use node as base image
FROM cerner/terra-node-ci:1

```

This docker container is intended for CI and as such is fairly traditional. Based on a node docker container, it copies the contents of the project and runs npm install to setup the project for testing.

To run tests against this container simply run the npm task you expect to run, for example using docker compose:

```yml
version: '3'

services:
  test-ci:
    build: ./
    command: 'npm run wdio-default'
```

```bash
docker-compose run -e FORM_FACTOR=tiny test-ci
```
