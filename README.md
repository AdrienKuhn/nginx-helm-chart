# nginx-helm-chart

This Helm chart will deploy a hardened [nginx](https://github.com/AdrienKuhn/hardened-nginx) instance.

## Configuration

Check the [values.yaml file](values.yaml) for all available configuration values.

| Variable                  | Description                                                           | Default                                                                                       |
| ------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| `replicaCount`            | The number of nginx replicas to run                                   | `1`                                                                                           |
| `image.repository`        | The repository containing the nginx image                             | `krewh/hardened-nginx`                                                                        |
| `image.tag`               | The docker image tag to deploy                                        | `1.1.1`                                                                                       |
| `image.pullPolicy`        | The image pull policy                                                 | `IfNotPresent`                                                                                |
| `imagePullSecrets`        | The configuration for imagePullSecrets                                | `[]`                                                                                          |
| `serviceAccount.create`   | Set to true to create a service account                               | `false`                                                                                       |
| `serviceAccount.name`     | The name for the service account. Automatically generated if not set. | `nil`                                                                                         |
| `podSecurityContext`      | The pod security context                                              | `{}`                                                                                          |
| `securityContext`         | The security context                                                  | `{}`                                                                                          |
| `livenessProbe`           | LivenessProbe configuration                                           | `{httpGet: {path: /, scheme: HTTPS, port: https},initialDelaySeconds: 10,periodSeconds: 10}`  |
| `readinessProbe`          | RedinessProbe configuration                                           | `{httpGet: {path: /, scheme: HTTPS, port: https},initialDelaySeconds: 5,periodSeconds: 2}`    |
| `serverBlock`             | Nginx server block configuration                                      | See [values.yaml](values.yaml)                                                                |
| `initContainers`          | init containers for the nginx pod                                     | `{}`                                                                                          |
| `volumeMounts`            | Volume to mount on the nginx container                                | `{}`                                                                                          |
| `volumes`                 | Volumes for the pod                                                   | `{}`                                                                                          |
| `service.type`            | Type of service to create for the Web interface                       | `ClusterIP`                                                                                   |
| `service.port`            | The port on which the SMTP service should listen                      | `443`                                                                                         |
| `ingress.enabled`         | Set to true to enable ingress                                         | `false`                                                                                       |
| `ingress.annotations`     | Annotations for ingress                                               | `{}`                                                                                          |
| `ingress.hosts`           | Hosts to configure for ingress                                        | `[]`                                                                                          |
| `ingress.tls`             | TLS configuration for ingress                                         | `[]`                                                                                          |
| `ressources`              | Allows you to set the resources for the Deployment                    | `{}`                                                                                          |
| `nodeSelector`            | Node labels for pod assignment	                                    | `{}`                                                                                          |
| `tolerations`             | Node taints to tolerate                                               | `[]`                                                                                          |
| `affinity`                | Node/pod affinities                                                   | `{}`                                                                                          |

## Installation

### Add repository

Follow instructions at [https://adrienkuhn.github.io/helm-repo/](https://adrienkuhn.github.io/helm-repo/)

### Install

```bash
helm install adrienkuhn-helm-repo/nginx \
 --name nginx \
 --namespace nginx
```
