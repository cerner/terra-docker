<!-- Logo -->
<p align="center">
  <img height="128" width="128" src="https://github.com/cerner/terra-docker/raw/master/terra.png">
</p>

<!-- Name -->
<h1 align="center">
  Terra Docker
</h1>

[![License](https://badgen.net/github/license/cerner/terra-docker)](https://github.com/cerner/terra-docker/blob/master/LICENSE)

# terra-docker

This is a repo for docker files supporting Terra CI and development.

This repo contains docker files to create the following images:

## terra-node-base

This dockerfile serves as a base for our CI and Dev docker containers. It provides a common version of node as well as some other common settings.

## terra-node-ci

This dockerfile provides a docker image for terra projects to extend to use in CI it will copy code as well as run npm install by default.

## terra-node-dev

This dockerfile provides a docker image setup with zshell for developers to use as a common node development environment. This image copies no code in and can be used directly with a volume mount to add code to the /opt/module directory.
