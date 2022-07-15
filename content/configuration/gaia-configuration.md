# Gaia configuration

Gaia can be configured :

* using property files (when running from source or with the `jar`)
* using environment variables (when running with the `jar` or in `docker`)

## Configuration parameters

|property                  |env var                     |usage                                  |default value                  |
|--------------------------|----------------------------|---------------------------------------|-------------------------------|
|server.port               |SERVER_PORT                 |Port on which Gaia listens             |8080                           |
|gaia.externalUrl          |GAIA_EXTERNAL_URL           |Externally reachable URL of Gaia       |http://localhost:${server.port}|
|gaia.mongodb.uri          |GAIA_MONGODB_URI            |URI to connect to the MongoDb database |mongodb://localhost:27017/gaia |
|gaia.defaultAdminPassword |GAIA_DEFAULT_ADMIN_PASSWORD |Default password of the _admin_ user   |admin123                       |