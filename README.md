# Simple Helm Chart for ML model deployments


## Introduction

This [Helm](https://github.com/kubernetes/helm) chart installs a serialized ML model API for predictions in a Kubernetes cluster.

## Prerequisites

- Kubernetes cluster 1.22+
- Helm 3.12.0+

## Installation

### Add Helm repository

```bash
helm repo add ml-service https://github.com/degrasse-python/ml-service
helm repo update
```

### Configure the chart

The following items can be set via `--set` flag during installation or configured by editing the `values.yaml` directly (need to download the chart first).

#### Configure the way how to expose mlflow service:

- **Ingress**: The ingress controller must be installed in the Kubernetes cluster.
- **ClusterIP**: Exposes the service on a cluster-internal IP. Choosing this value makes the service only reachable from within the cluster.
- **NodePort**: Exposes the service on each Node’s IP at a static port (the NodePort). You’ll be able to contact the NodePort service, from outside the cluster, by requesting `NodeIP:NodePort`.
- **LoadBalancer**: Exposes the service externally using a cloud provider’s load balancer.

### Install the chart

Install the ml-service helm chart with a release name `my-release`:

```bash
helm install --name my-release ml-service/ml-service
```

## Uninstallation

To uninstall/delete the `my-release` deployment:

```bash
helm delete --purge my-release
```

## Configuration

The following table lists the configurable parameters of the mlflow chart and the default values.

| Parameter                          | Description                                         | Default                                                                |
| ---------------------------------- | --------------------------------------------------- | ---------------------------------------------------------------------- |
| **Image**                          |
| `image.repository`                 | MLFlow Image name                                   | `ayadi05/mlflow`                                                       |
| `image.tag`                        | MLFlow Image tag                                    | `1.5.0`                                                                |
| `image.pullPolicy`                 | MLFlow Image pull policy                            | `IfNotPresent`                                                         |
| **Service**                        |
| `service.type`                     | Type of service for MLFlow frontend                 | `ClusterIP`                                                             |
| `service.port`                     | Port to expose service                              | `443`                                                                   |
| `service.targetPort`                 | Port where the service is reachable                 | `8080`                                                                |
| `service.tls`           | tls if service type is `enabled`    | `true`                                                                  |
| **Ingress**                        |
| `ingress.enabled`                  | Enables Ingress                                     | `false`                                                                |
| `ingress.annotations`              | Ingress annotations                                 | `{}`                                                                   |
| `ingress.path`                     | Path to access mlapi                             | `/`                                                                    |
| `ingress.hosts`                    | Ingress hosts                                       | `[]`                                                                   |
| `ingress.tls`                      | Ingress TLS configuration                           | `[]`                                                                   |
| **Resources**                      |
| `resources`                        | CPU/Memory resource requests/limits                 | `{}`                                                                   |

## Contributing

At the moment we are not taking any pull requests because this is just an example for folks to use for inspo.

## License

[MIT](/LICENSE.md)
