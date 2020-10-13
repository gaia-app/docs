# Database configuration

There are multiple ways of configuring the database connection used by Gaia, depending one how Gaia is started.

## source & docker-compose

When starting Gaia using source code and docker-compose, a MongoDb database is created alongside Gaia, and Gaia is configured directly to use it:

```yml
version: "3"
services:
    gaia:
        build: .
        image: gaia
        ports:
            - '8080:8080'
        environment:
            - "GAIA_MONGODB_URI=mongodb://mongo/gaia"
            - "GAIA_EXTERNAL_URL=http://172.17.0.1:8080"
        volumes:
            - /var/run/docker.sock:/var/run/docker.sock

    mongo:
        build:
            context: .
            dockerfile: ./Dockerfile-db
        image: gaia-db
```

To use a different MongoDb instance, replace the `GAIA_MONGODB_URI` environment variable with the URI of your database, and remove the provided MongoDb instance.
If your database uses user/password authentication, pass them in the URL as well :

```yml
version: "3"
services:
    gaia:
        build: .
        image: gaia
        ports:
            - '8080:8080'
        environment:
            - "GAIA_MONGODB_URI=mongodb+srv://gaia:gaia_database_password@gaia-gcp-europe-west1-azerty.gcp.mongodb.net/gaia?retryWrites=true&w=majority"
            - "GAIA_EXTERNAL_URL=http://172.17.0.1:8080"
        volumes:
            - /var/run/docker.sock:/var/run/docker.sock
```

## docker

When starting Gaia using docker, use environment variables to setup MongoDb URI :

```bash
docker run -d \
  --name gaia-server \
  -e GAIA_MONGODB_URI=mongodb+srv://gaia:gaia_database_password@gaia-gcp-europe-west1-azerty.gcp.mongodb.net/gaia?retryWrites=true&w=majority
  gaia-app/gaia
```

## jar

When starting Gaia using the `jar`, you can change the MongoDb URI using JVM parameters :

```bash
java -jar gaia.jar -Dgaia.mongodb.uri=mongodb+srv://gaia:gaia_database_password@gaia-gcp-europe-west1-azerty.gcp.mongodb.net/gaia?retryWrites=true&w=majority
```