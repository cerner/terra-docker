# terra-node-ci

This dockerfile provides a docker image for terra projects to extend to use in CI it will copy code as well as run npm install by default.

## API (of a sort)

* Extends terra-node-base
* On build: Copies . to /opt/module
* On build: Runs Npm Install

## Usage

This docker image is intended for CI and as such is fairly traditional. This docker image is expected to be defined as the base image for a project specific Dockerfile; see example below.

```dockerfile
# use node as base image
FROM cerner/terra-node-ci:1

```

Then, when the above Dockerfile is used to build the project-specific docker container, the resulting docker container is based on a node docker container, it copies the contents of the project and runs npm install to setup the project for testing.

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
