# Gaia Runner configuration

The Gaia runner can be configured :

- using property files (when running from source or with the `jar`)
- using environment variables (when running with the `jar` in `docker`, or in `kubernetes`)

## Configuration parameters

| property                 | env var                  | usage                                                                  | default value           |
| ------------------------ | ------------------------ | ---------------------------------------------------------------------- | ----------------------- |
| gaia.url                 | GAIA_URL                 | URL of the Gaia server                                                 | `http://localhost:8080` |
| gaia.runner.concurrency  | GAIA_RUNNER_CONCURRENCY  | Number of jobs the Gaia Runner can run in parallel                     | `10`                    |
| gaia.runner.api.username | GAIA_RUNNER_API_USERNAME | Username to access Gaia API for the Runner                             | `gaia-runner`           |
| gaia.runner.api.password | GAIA_RUNNER_API_PASSWORD | Password to access Gaia API for the Runner                             |                         |
| gaia.runner.executor     | GAIA_RUNNER_EXECUTOR     | The executor to use for the Runner. Valid values are `docker` or `k8s` | `docker`                |

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

By default, The Gaia Runner uses `docker` to run the Terraform modules.

#### Using local docker daemon

| property                     | env var                      | usage                           | default value               |
| ---------------------------- | ---------------------------- | ------------------------------- | --------------------------- |
| gaia.runner.docker.daemonUrl | GAIA_RUNNER_DOCKER_DAEMONURL | URL of the Docker Daemon to use | unix:///var/run/docker.sock |

### Kubernetes Runner

When the property `gaia.runner.executor` is set to `k8s`, the Runner will use the Kubernetes API to run the Terraform modules.
Terraform modules are runned as simple *Pods*.
If the Runner is running inside a Kubernetes cluster, it will try to use this cluster to run its pods.
To do so, some RBAC roles and a Kubernetes *ServiceAccount* for the Runner should be configured to allow the Runner to start new pods, attach to them, and delete them.

!!! info
    An experimental Helm chart is available [on Github](https://github.com/gaia-app/chart)

#### Namespace configuration
By default, it will use the namespace the Runner is deployed in to run the Terraform pods, if the Runner runs in a kubernetes cluster. Otherwise, the `gaia.runner.k8s.namespace` should be set.
This namespace configuration can be overrided.

#### Properties

| property                  | env var                   | usage                                         | default value        |
| ------------------------- | ------------------------- | --------------------------------------------- | -------------------- |
| gaia.runner.k8s.namespace | GAIA_RUNNER_K8S_NAMESPACE | Kubernetes namespace to use when running pods | in-cluster namespace |

#### RBAC

Gaia Runner needs the following RBAC roles to work properly:

| apiGroups | resource      | verbs               | usage                            |
|-----------|---------------|---------------------|----------------------------------|
| ""        | pods          | create, get, delete | to run gaia jobs in pods         |
| ""        | "pods/attach" | create, get         | to send terraform script in pods |
| ""        | "pods/logs"   | get                 | to read the logs                 |

Below is a sample Kubernetes *Role* with the needed RBAC roles:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: gaia-runner-role
rules:
- apiGroups: [""]
  resources: ["pods",]
  verbs: ["create", "get", "delete"]
- apiGroups: [""]
  resources: ["pods/attach"]
  verbs: ["create", "get"]
- apiGroups: [""]
  resources: ["pods/log"]
  verbs: ["get"]
```

And the associated *RoleBinding*:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: gaia-runner-role-binding
subjects:
- kind: ServiceAccount
  name: gaia-runner
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: gaia-runner-role
  apiGroup: rbac.authorization.k8s.io
```

