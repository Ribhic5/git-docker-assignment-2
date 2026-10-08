# Git and Docker Starter Application

This repository contains a small Python web application used to practice Git, GitHub, and Docker workflows.

## Application

The application listens on port 8000 and returns a text response when accessed over HTTP.

## Verification

Verify the application through localhost on host port 8080, mapped to container port 8000.
Verify that the application response includes Status: healthy - ribhia.

## Usage

Keep Docker Desktop running before building or starting containers.

Build the image from the project directory:

```bash
docker build -t git-docker-app:test .
```

Start the application with host port 8080 mapped to container port 8000:

```bash
docker run -d --name app-test -p 8080:8000 git-docker-app:test
```

Once the application starts, request its response:

```bash
curl http://localhost:8080
```

Expected response:

```text
Advanced Git Docker App
Status: healthy - ribhia
```

View the application logs and clean up when finished:

```bash
docker logs app-test
docker stop app-test
docker rm app-test
```

## Container Network Verification

Create a network and start the application on it:

```bash
docker network create app-net
docker run -d --name app-test --network app-net git-docker-app:test
```

Once the application starts, verify access by container name:

```bash
docker run --rm --name network-test --network app-net curlimages/curl:8.5.0 http://app-test:8000
```

Remove the application container and network afterward:

```bash
docker stop app-test
docker rm app-test
docker network rm app-net
```
