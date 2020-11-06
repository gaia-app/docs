# Gaia Runner configuration

The Gaia runner can be configured :

* using property files (when running from source or with the `jar`)
* using environment variables (when running with the `jar` or in `docker`)

## Configuration parameters

|property|env var|usage|default value|
|--------|-----|-------------|-------|
|gaia.url|GAIA_URL|URL of the Gaia server|http://localhost:8080|
|gaia.runner.concurrency|GAIA_RUNNER_CONCURRENCY|Number of jobs the Gaia Runner can run in parallel|10|
|gaia.runner.api.username|GAIA_RUNNER_API_USERNAME|Username to access Gaia API for the Runner|gaia-runner|
|gaia.runner.api.password|GAIA_RUNNER_API_PASSWORD|Password to access Gaia API for the Runner||

The `gaia.runner.api.password` is mandatory.
If not set, the following message will show to the console when starting the runner : 

```text
***************************
APPLICATION FAILED TO START
***************************

Description:

Binding to target org.springframework.boot.context.properties.bind.BindException: Failed to bind properties under 'gaia.runner.api' to io.gaia_app.runner.config.RunnerConfigurationProperties$RunnerApiProperties failed:

    Property: gaia.runner.api.password
    Value: null
    Reason: must not be blank


Action:

Update your application's configuration
```

### Docker Runner

The Gaia runner uses `docker` to run the Terraform modules.

#### Using local docker daemon

|property|env var|usage|default value|
|--------|-----|-------------|-------|
|gaia.runner.docker.daemonUrl|GAIA_RUNNER_DOCKER_DAEMONURL|URL of the Docker Daemon to use|unix:///var/run/docker.sock|