# Github integration

This page describes how to configure Gaia to integrate with Github to:

* be able to login using a Github account
* be able to import Terraform modules directly from Github

!!! note
    only **public** repositories of the Github user can be imported for now.

## Create a Github OAuth App

On Github, create a new OAuth App (in an organization or in your personnal account).

Go to https://github.com/settings/developers, and click _Register a new application_.

![Screenshot of OAuth Apps screen on Github](./github-integration/oauth-apps.png)

Enter the following information:

* Application name : Gaia
* Homepage URL : The URL of your Gaia instance (http://localhost:8080 if running a development instance)
* Application description: Gaia
* Authorization callback URL : Homepage URL + /auth/oauth2/github/callback

![Screenshot of OAuth App creation screen on Github](./github-integration/new-oauth-app.png)

Take note of the _Client ID_, generate a _Client secret_, and take note of it too.

![Screenshot the OAuth App showing Client ID and Client Secret on Github](./github-integration/oauth-app-with-secret.png)

## Configure Gaia for Github

### With docker-compose

Edit the `application-github.properties` file in the `src/main/resources` directory to add your _Client ID_ and _Client Secret_ for the Github registration.

```properties
spring.security.oauth2.client.registration.github.client-id=<CLIENT_ID>
spring.security.oauth2.client.registration.github.client-secret=<CLIENT_SECRET>
```

Edit your `docker-compose.yml` file to activate the `github` Spring profile:

```yaml
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
      - "GAIA_RUNNER_API_PASSWORD=123456"
      - "SPRING_PROFILES_ACTIVE=github"
  mongo:
    build:
      context: .
      dockerfile: ./Dockerfile-db
    image: gaia-db
```

## Login with Github

On the _Login_ page, the _github_ button should appear:

![Screenshot the login page on Gaia](./github-integration/login-with-github.png)

## Import a module from Github

On the _Import Module_ page, you should now be able to select a module from the repositories of your Github user.

![Screenshot the login page on Gaia](./github-integration/import-module-from-github.png)