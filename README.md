# Backrest Helm Chart

[![GitHub](https://img.shields.io/github/license/RobertoBochet/backrest-chart?style=flat-square)](https://github.com/RobertoBochet/backrest-chart)
[![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/RobertoBochet/backrest-chart/release.yml?label=publish%20chart&style=flat-square)](https://github.com/RobertoBochet/scraper-bot/pkgs/container/backrest-chart)

This repo provides the (unofficial) helm chart for [Backrest](https://github.com/garethgeorge/backrest)

## Deploy

Helm chart package is available in the github OCI registry
```
oci://ghcr.io/robertobochet/backrest-chart
```
You can use it to directly deploy on your kubernetes cluster
1. Retrieve the default values file
   ```shell
   helm show values oci://ghcr.io/robertobochet/backrest-chart > values.yaml
   ```
2. Customize the `values.yaml`
3. Install backrest
   ```shell
   helm install scraper-bot oci://ghcr.io/robertobochet/backrest-chart -f values.yaml
   ```

## Parameters

### Common parameters

| Name               | Description                                        | Value |
| ------------------ | -------------------------------------------------- | ----- |
| `nameOverride`     | String to partially override common.names.fullname | `""`  |
| `fullnameOverride` | String to fully override common.names.fullname     | `""`  |
| `imagePullSecrets` | Secret to use for pulling the image                | `[]`  |

### Image

| Name               | Description                                                   | Value                   |
| ------------------ | ------------------------------------------------------------- | ----------------------- |
| `image.registry`   | image registry, e.g. gcr.io,docker.io                         | `""`                    |
| `image.repository` | Image to start for this pod                                   | `garethgeorge/backrest` |
| `image.tag`        | Visit: Image tag. Defaults to `appVersion` within Chart.yaml. | `""`                    |
| `image.pullPolicy` | Image pull policy                                             | `IfNotPresent`          |

### Security

| Name                 | Description          | Value |
| -------------------- | -------------------- | ----- |
| `podSecurityContext` | Pod security context | `{}`  |
| `securityContext`    | Security context     | `{}`  |

### Service

| Name                               | Description                                                                                                                                                                                          | Value       |
| ---------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| `service.type`                     | Kubernetes service type for http traffic                                                                                                                                                             | `ClusterIP` |
| `service.port`                     | Port number for web traffic                                                                                                                                                                          | `9898`      |
| `service.clusterIP`                | ClusterIP setting for http autosetup for deployment is None                                                                                                                                          | `None`      |
| `service.loadBalancerIP`           | LoadBalancer IP setting                                                                                                                                                                              | `nil`       |
| `service.nodePort`                 | NodePort for http service                                                                                                                                                                            | `nil`       |
| `service.externalTrafficPolicy`    | If `service.type` is `NodePort` or `LoadBalancer`, set this to `Local` to enable source IP preservation                                                                                              | `nil`       |
| `service.externalIPs`              | External IPs for service                                                                                                                                                                             | `nil`       |
| `service.ipFamilyPolicy`           | HTTP service dual-stack policy                                                                                                                                                                       | `nil`       |
| `service.ipFamilies`               | HTTP service dual-stack familiy selection,for dual-stack parameters see official kubernetes [dual-stack concept documentation](https://kubernetes.io/docs/concepts/services-networking/dual-stack/). | `nil`       |
| `service.loadBalancerSourceRanges` | Source range filter for http loadbalancer                                                                                                                                                            | `[]`        |
| `service.annotations`              | HTTP service annotations                                                                                                                                                                             | `{}`        |
| `service.labels`                   | HTTP service additional labels                                                                                                                                                                       | `{}`        |
| `service.loadBalancerClass`        | Loadbalancer class                                                                                                                                                                                   | `nil`       |

### Ingress

| Name                                 | Description                                                                 | Value                    |
| ------------------------------------ | --------------------------------------------------------------------------- | ------------------------ |
| `ingress.enabled`                    | Enable ingress                                                              | `false`                  |
| `ingress.className`                  | Ingress class name                                                          | `""`                     |
| `ingress.annotations`                | Ingress annotations                                                         | `{}`                     |
| `ingress.hosts[0].host`              | Default Ingress host                                                        | `backrest.example.local` |
| `ingress.hosts[0].paths[0].path`     | Default Ingress path                                                        | `/`                      |
| `ingress.hosts[0].paths[0].pathType` | Ingress path type                                                           | `Prefix`                 |
| `ingress.tls`                        | Ingress tls settings                                                        | `[]`                     |
| `ingress.apiVersion`                 | Specify APIVersion of ingress object. Mostly would only be used for argocd. |                          |

### deployment

| Name                                 | Description                                                       | Value                   |
| ------------------------------------ | ----------------------------------------------------------------- | ----------------------- |
| `resources`                          | Kubernetes resources                                              | `{}`                    |
| `podAnnotations`                     | Annotations                                                       | `{}`                    |
| `startupProbe.enabled`               | Enable startupProbe                                               | `true`                  |
| `startupProbe.initialDelaySeconds`   | Initial delay seconds for startupProbe                            | `10`                    |
| `startupProbe.periodSeconds`         | Period seconds for startupProbe                                   | `10`                    |
| `startupProbe.timeoutSeconds`        | Timeout seconds for startupProbe                                  | `1`                     |
| `startupProbe.failureThreshold`      | Failure threshold for startupProbe                                | `3`                     |
| `startupProbe.successThreshold`      | Success threshold for startupProbe                                | `1`                     |
| `livenessProbe.enabled`              | Enable livenessProbe                                              | `true`                  |
| `livenessProbe.initialDelaySeconds`  | Initial delay seconds for livenessProbe                           | `10`                    |
| `livenessProbe.periodSeconds`        | Period seconds for livenessProbe                                  | `10`                    |
| `livenessProbe.timeoutSeconds`       | Timeout seconds for livenessProbe                                 | `1`                     |
| `livenessProbe.failureThreshold`     | Failure threshold for livenessProbe                               | `3`                     |
| `livenessProbe.successThreshold`     | Success threshold for livenessProbe                               | `1`                     |
| `readinessProbe.enabled`             | Enable readinessProbe                                             | `true`                  |
| `readinessProbe.initialDelaySeconds` | Initial delay seconds for readinessProbe                          | `10`                    |
| `readinessProbe.periodSeconds`       | Period seconds for readinessProbe                                 | `10`                    |
| `readinessProbe.timeoutSeconds`      | Timeout seconds for readinessProbe                                | `1`                     |
| `readinessProbe.failureThreshold`    | Failure threshold for readinessProbe                              | `3`                     |
| `readinessProbe.successThreshold`    | Success threshold for readinessProbe                              | `1`                     |
| `nodeSelector`                       | NodeSelector for the deployment                                   | `{}`                    |
| `tolerations`                        | Tolerations for the deployment                                    | `[]`                    |
| `affinity`                           | Affinity for the deployment                                       | `{}`                    |
| `config`                             | Backrest configuration pass to container as environment variables |                         |
| `config.BACKREST_DATA`               | Backrest data path                                                | `/backrest/data`        |
| `config.BACKREST_CONFIG`             | Backrest config path                                              | `/backrest/config.json` |
| `config.BACKREST_PORT`               | Backrest webapp port                                              | `0.0.0.0:9898`          |
| `env`                                | Additional environment variables to pass to containers            | `[]`                    |

### ServiceAccount

| Name                                          | Description                                                                                                                               | Value   |
| --------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ------- |
| `serviceAccount.create`                       | Enable the creation of a ServiceAccount                                                                                                   | `false` |
| `serviceAccount.name`                         | Name of the created ServiceAccount, defaults to release name. Can also link to an externally provided ServiceAccount that should be used. | `""`    |
| `serviceAccount.automountServiceAccountToken` | Enable/disable auto mounting of the service account token                                                                                 | `false` |
| `serviceAccount.imagePullSecrets`             | Image pull secrets, available to the ServiceAccount                                                                                       | `[]`    |
| `serviceAccount.annotations`                  | Custom annotations for the ServiceAccount                                                                                                 | `{}`    |
| `serviceAccount.labels`                       | Custom labels for the ServiceAccount                                                                                                      | `{}`    |

### Persistence

| Name                                              | Description                                                                                           | Value               |
| ------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ------------------- |
| `persistence.enabled`                             | Enable persistent storage                                                                             | `true`              |
| `persistence.claimName`                           | Use an existing claim to store repository information                                                 | `backrest-storage`  |
| `persistence.size`                                | Size for persistence to store repo information                                                        | `10Gi`              |
| `persistence.accessModes`                         | AccessMode for persistence                                                                            | `["ReadWriteOnce"]` |
| `persistence.labels`                              | Labels for the persistence volume claim to be created                                                 | `{}`                |
| `persistence.annotations.helm.sh/resource-policy` | Resource policy for the persistence volume claim                                                      | `keep`              |
| `persistence.storageClass`                        | Name of the storage class to use                                                                      | `nil`               |
| `persistence.subPath`                             | Subdirectory of the volume to mount at                                                                | `nil`               |
| `persistence.volumeName`                          | Name of persistent volume in PVC                                                                      | `""`                |
| `cache`                                           | Volume for cache                                                                                      |                     |
| `extraVolumes`                                    | Additional volumes to mount to the Gitea deployment                                                   | `[]`                |
| `extraContainerVolumeMounts`                      | Mounts that are only mapped into the Gitea runtime/main container, to e.g. override custom templates. | `[]`                |

### Miscellaneous

| Name           | Description                            | Value |
| -------------- | -------------------------------------- | ----- |
| `extraObjects` | Array of extra K8s manifests to deploy | `[]`  |
