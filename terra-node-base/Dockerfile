# This dockerfile serves as a base for our CI and Dev docker containers. It provides a common version of node as well as some other common settings.
FROM node:erbium-alpine

# Open up port 8080
EXPOSE 8080

# Node env variable for testing, Indicates that we should not spin up a docker instance when running tests.
ENV CI true

# Setting unsafe-perm true to allow installing to root. This docker container is not suitible for production use.
RUN npm config set unsafe-perm true -g \
  # Git is needed for both ci and development.
  && apk add git

WORKDIR /opt/module
