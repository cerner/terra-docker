<!-- Logo -->
<p align="center">
  <img height="128" width="128" src="https://github.com/cerner/terra-docker/raw/main/terra.png">
</p>

<!-- Name -->
<h1 align="center">
  Terra Docker
</h1>

[![License](https://badgen.net/github/license/cerner/terra-docker)](https://github.com/cerner/terra-docker/blob/main/LICENSE)

# terra-docker

This is a repo for docker files supporting Terra CI and development.

This repo contains docker files to create the following images:

## terra-node-base

This dockerfile serves as a base for our CI and Dev docker containers. It provides a common version of node as well as some other common settings. It is based on node 12 Alpine.

## terra-node-ci

This dockerfile provides a docker image for terra projects to extend to use in CI it will copy code as well as run npm install by default.

## terra-node-dev

This dockerfile provides a docker image setup with zshell for developers to use as a common node development environment. This image copies no code in and can be used directly with a volume mount to add code to the /opt/module directory.

## Versioning

These docker containers are versioned via [semver](https://medium.com/@mccode/using-semantic-versioning-for-docker-image-tags-dfde8be06699).

## Development notes

### Changes to terra-node-base

Make any changes to terra-node-base in an isolated pull request. Automated releases through docker hub are non deterministic and there is no guarantee that terra-node-base will build and be released before the containers that depend on it.

### Releases

Are handled by docker hub based on tags.

To release terra-node-base tag a branch with `terra-node-base@v#.#` where `#.#` is the version you wish to release.

To release terra-node-ci tag a branch with `terra-node-ci@v#.#` where `#.#` is the version you wish to release.

To release terra-node-dev tag a branch with `terra-node-base@v#.#` where `#.#` is the version you wish to release.

All release will release a latest tag and a tag based on the major version. 1.1 would be released with a 1 tag, 2.2 would be released with a 2 tag, etc.
