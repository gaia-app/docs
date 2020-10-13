# QuickStart

## Pre-requisites

Gaia needs : 

 * a docker daemon (used to run Terraform itself)
 * a MongoDb database (to store its data)

## Getting started with docker

### Using source-code and docker-compose

Clone the Gaia repository : 

```bash
git clone git@github.com:gaia-app/gaia.git
```

Run docker-compose :

```bash
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
