# Docker Swagger UI

[![Docker Build Status](https://img.shields.io/docker/build/metz/swaggerui.svg)](https://hub.docker.com/r/metz/swaggerui/)
[![Docker Automated build](https://img.shields.io/docker/automated/metz/swaggerui.svg)](https://hub.docker.com/r/metz/swaggerui/)

`metz/swaggerui` is a Docker image for the [Swagger UI](https://swagger.io/swagger-ui/), that supports publishing [Swagger Specs](https://swagger.io/specification/) via **API** and **volume mount**.

## Getting started

You can pull and run a pre-built Docker image directly from [Dockerhub](https://hub.docker.com/r/metz/swaggerui/):

```sh
docker run --name swaggerui -p 80:8080 metz/swaggerui
```

This will start the Swagger UI using the default [petstore JSON](http://petstore.swagger.io/v2/swagger.json). Then you can access the Swagger UI directly from a browser:

- **Swagger UI:** [http://localhost:80/](http://localhost/)

### Publish a custom Swagger Spec

In order to supply your own Swagger Spec (`swagger.json`), you will need to either publish it via the **API** or mount it with a **volume**.

Both solutions can be combined, so that the currently published Swagger Spec will be synced with the mounted directory.

#### API

> For more details about the API, see the [API overview](#api-reference).

A new Swagger Spec can be published by sending a `POST` request with the Swagger JSON in the body to the `/publish` endpoint:

```sh
curl -v -X POST \
	-d @swagger_upload.json \
	-H "Content-Type: application/json" \
	http://localhost:80/publish
```

#### Volume

In order to publish the Swagger Spec via filesystem, mount the directory containing the `swagger.json` as a volume at `/swaggerui/swagger`:

```sh
docker run --name swaggerui -p 80:8080 -v /path/to/spec:/swaggerui/swagger metz/swaggerui
```

##### Persistence

Mounting the volume also preserves the Swagger Spec across container shutdown and startup.

## Developing

### Built With

Technology | Version
---------- | -------
Swagger UI | 3.2.2
NodeJS     | 8

> Swagger UI only supports the Swagger / OpenAPI specification `2.0` as of version `3.x`.

### Building

In order to build the container manually, execute the following in the checkout directory:

```sh
docker build -t metz/swaggerui .
```

## API Reference

This Docker image provides a simple API that allows to retrieve and update the current Swagger Spec that will be displayed by Swagger UI.

Method | Endpoint   | Description
------ | ---------- | -----------
`GET`  | `/`        | Swagger UI
`GET`  | `/spec`    | Current Swagger specification
`POST` | `/publish` | Publish a new Swagger specification

## Supported tags

> Find all available tags on [Dockerhub](https://hub.docker.com/r/metz/swaggerui/tags/).

Each `metz/swaggerui` version is tagged. We also have 2 tags for the beta and stable track:

- `latest`: latest stable build, this is the latest officially supported release
- `nightly`: images built from HEAD periodically. Potentially unstable!

For more information about this image and the functionality it provides, please see the [`docker-swaggerui`](https://github.com/christianmetz/docker-swaggerui) GitHub repository.

## Licensing

A Project by Christian Metz.  
Released under the [MIT License](LICENSE).
