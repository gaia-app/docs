# QuickStart

## Pre-requisites

Gaia needs : 

 * a Docker daemon (used to run Terraform itself)
 * a MongoDb database (to store its data)

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
