# QuickStart

## Pre-requisites

Gaia needs : 

 * a Docker daemon (used to run Terraform itself)
 * a MongoDb database (to store its data)

## Getting started with docker-compose

Create the following `docker-compose.yml` file

```yaml
version: "3.9"
services:
  gaia:
    image: "gaiaapp/gaia"
    ports: 
      - "8080:8080"
    environment:
      - "GAIA_MONGODB_URI=mongodb://mongo/gaia"
      - "GAIA_RUNNER_API_PASSWORD=123456"
  runner:
    image: "gaiaapp/runner"
    environment:
      - "GAIA_URL=http://gaia:8080"
      - "GAIA_RUNNER_API_PASSWORD=123456"
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock"
  mongo:
    image: "mongo:4.4"
```

Then, run `docker-compose up -d`.
When Gaia is started, open https://localhost:8080 on your browser.

## Getting started with source-code & Docker

### Using docker-compose

The Gaia source code contains several docker-compose files to help users getting started quickly.

#### Start Gaia & a MongoDb database

Clone the Gaia repository & run docker-compose: 

```bash
git clone git@github.com:gaia-app/gaia.git
cd gaia
docker-compose up -d
```

#### Start Gaia-Runner

Clone the runner repository & run docker-compose: 

```bash
git clone git@github.com:gaia-app/runner.git
cd runner
docker-compose up -d
```

## Login

Go to [http://localhost:8080](http://localhost:8080)

Default credentials are :

 * admin account with `ROLE_ADMIN`

```
username: admin
password: admin123
```

 * user account with `ROLE_USER`

```
username: user
password: user123
```
