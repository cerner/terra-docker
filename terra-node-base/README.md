# terra-node-base

This dockerfile serves as a base for our CI and Dev docker containers. It provides a common version of node as well as some other common settings. It is based on node 12 Alpine.

## API (of a sort):

* Workdir: /opt/module
* Exposed Port: 8080
* git: installed

## Usage

This docker container is not intended for outside consumption. It provides a common version of node and other common setup to the `terra-node-ci` and `terra-node-dev` docker containers.
