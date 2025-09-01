# Backrest (unofficial) Helm Chart

[![GitHub](https://img.shields.io/github/license/RobertoBochet/backrest-chart?style=flat-square)](https://github.com/RobertoBochet/backrest-chart)
[![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/RobertoBochet/backrest-chart/release.yml?label=publish%20chart&style=flat-square)](https://github.com/RobertoBochet/scraper-bot/pkgs/container/backrest-chart)
[![GitHub Latest Release Version](https://img.shields.io/github/v/release/RobertoBochet/backrest-chart?sort=semver&display_name=release&style=flat-square)](https://github.com/RobertoBochet/backrest-chart/releases)
[![Static Badge](https://img.shields.io/badge/-backrest-w?style=flat-square&logo=artifacthub&logoColor=white&logoSize=18&label=Artifact%20Hub&labelColor=417598&color=2D4857)](https://artifacthub.io/packages/helm/robertobochet/backrest)

[Backrest](https://github.com/garethgeorge/backrest) is a web UI and orchestrator for [restic](https://restic.net/) backup.

## Deploy

1. Add the repository to helm
   ```shell
   helm repo add robertobochet https://robertobochet.github.io/charts
   helm repo update
   ```
2. Retrieve the default values file
   ```shell
   helm show values robertobochet/backrest > values.yaml
   ```
3. Customize the `values.yaml`
4. Install backrest
   ```shell
   helm install scraper-bot robertobochet/backrest -f values.yaml
   ```

## Parameters

### Common parameters

| Name               | Description                                        | Value |
| ------------------ | -------------------------------------------------- | ----- |
| `nameOverride`     | String to partially override common.names.fullname | `""`  |
| `fullnameOverride` | String to fully override common.names.fullname     | `""`  |
| `imagePullSecrets` | Secret to use for pulling the image                | `[]`  |
| `replicaCount`     | number of replicas for the deployment              | `1`   |

### strategy

| Name                                    | Description    | Value      |
| --------------------------------------- | -------------- | ---------- |
| `strategy.type`                         | strategy type  | `Recreate` |
| `strategy.rollingUpdate.maxSurge`       | maxSurge       | `100%`     |
| `strategy.rollingUpdate.maxUnavailable` | maxUnavailable | `0`        |

### Image

| Name               | Description                                                   | Value                   |
| ------------------ | ------------------------------------------------------------- | ----------------------- |
| `image.registry`   | image registry, e.g. gcr.io,docker.io                         | `docker.io`             |
| `image.repository` | Image to start for this pod                                   | `garethgeorge/backrest` |
| `image.tag`        | Visit: Image tag. Defaults to `appVersion` within Chart.yaml. | `""`                    |
| `image.pullPolicy` | Image pull policy                                             | `IfNotPresent`          |

### Security

| Name                       | Description          | Value |
| -------------------------- | -------------------- | ----- |
| `podSecurityContext`       | Pod security context | `{}`  |
| `containerSecurityContext` | Security context     | `{}`  |

### Service

| Name                               | Description                                                                                                                                                                                          | Value       |
| ---------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| `service.type`                     | Kubernetes service type for http traffic                                                                                                                                                             | `ClusterIP` |
| `service.port`                     | Port number for web traffic                                                                                                                                                                          | `9898`      |
| `service.clusterIP`                | ClusterIP setting for http autosetup for deployment is None                                                                                                                                          | `None`      |
| `service.loadBalancerIP`           | LoadBalancer IP setting                                                                                                                                                                              | `""`        |
| `service.nodePort`                 | NodePort for http service                                                                                                                                                                            | `""`        |
| `service.externalTrafficPolicy`    | If `service.type` is `NodePort` or `LoadBalancer`, set this to `Local` to enable source IP preservation                                                                                              | `""`        |
| `service.externalIPs`              | External IPs for service                                                                                                                                                                             | `[]`        |
| `service.ipFamilyPolicy`           | HTTP service dual-stack policy                                                                                                                                                                       | `""`        |
| `service.ipFamilies`               | HTTP service dual-stack familiy selection,for dual-stack parameters see official kubernetes [dual-stack concept documentation](https://kubernetes.io/docs/concepts/services-networking/dual-stack/). | `[]`        |
| `service.loadBalancerSourceRanges` | Source range filter for http loadbalancer                                                                                                                                                            | `[]`        |
| `service.annotations`              | HTTP service annotations                                                                                                                                                                             | `{}`        |
| `service.labels`                   | HTTP service additional labels                                                                                                                                                                       | `{}`        |
| `service.loadBalancerClass`        | Loadbalancer class                                                                                                                                                                                   | `""`        |

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

| Name                                 | Description                                                            | Value                                             |
| ------------------------------------ | ---------------------------------------------------------------------- | ------------------------------------------------- |
| `resources`                          | Kubernetes resources                                                   | `{}`                                              |
| `podAnnotations`                     | Annotations                                                            | `{}`                                              |
| `startupProbe.enabled`               | Enable startupProbe                                                    | `true`                                            |
| `startupProbe.initialDelaySeconds`   | Initial delay seconds for startupProbe                                 | `10`                                              |
| `startupProbe.periodSeconds`         | Period seconds for startupProbe                                        | `10`                                              |
| `startupProbe.timeoutSeconds`        | Timeout seconds for startupProbe                                       | `1`                                               |
| `startupProbe.failureThreshold`      | Failure threshold for startupProbe                                     | `3`                                               |
| `startupProbe.successThreshold`      | Success threshold for startupProbe                                     | `1`                                               |
| `livenessProbe.enabled`              | Enable livenessProbe                                                   | `true`                                            |
| `livenessProbe.initialDelaySeconds`  | Initial delay seconds for livenessProbe                                | `10`                                              |
| `livenessProbe.periodSeconds`        | Period seconds for livenessProbe                                       | `10`                                              |
| `livenessProbe.timeoutSeconds`       | Timeout seconds for livenessProbe                                      | `1`                                               |
| `livenessProbe.failureThreshold`     | Failure threshold for livenessProbe                                    | `3`                                               |
| `livenessProbe.successThreshold`     | Success threshold for livenessProbe                                    | `1`                                               |
| `readinessProbe.enabled`             | Enable readinessProbe                                                  | `true`                                            |
| `readinessProbe.initialDelaySeconds` | Initial delay seconds for readinessProbe                               | `10`                                              |
| `readinessProbe.periodSeconds`       | Period seconds for readinessProbe                                      | `10`                                              |
| `readinessProbe.timeoutSeconds`      | Timeout seconds for readinessProbe                                     | `1`                                               |
| `readinessProbe.failureThreshold`    | Failure threshold for readinessProbe                                   | `3`                                               |
| `readinessProbe.successThreshold`    | Success threshold for readinessProbe                                   | `1`                                               |
| `nodeSelector`                       | NodeSelector for the deployment                                        | `{}`                                              |
| `tolerations`                        | Tolerations for the deployment                                         | `[]`                                              |
| `affinity`                           | Affinity for the deployment                                            | `{}`                                              |
| `config`                             | Backrest configuration forwarded to container as environment variables |                                                   |
| `config.BACKREST_DATA`               | Backrest data path                                                     | `{{ .Values.persistence.mountPath }}/data`        |
| `config.BACKREST_CONFIG`             | Backrest config path                                                   | `{{ .Values.persistence.mountPath }}/config.json` |
| `config.BACKREST_PORT`               | Backrest webapp port                                                   | `0.0.0.0:{{ .Values.service.port}}`               |
| `config.XDG_CACHE_HOME`              | Backrest cache path                                                    | `{{ .Values.cache.mountPath }}`                   |
| `env`                                | Additional environment variables to pass to containers                 | `[]`                                              |

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
| `persistence.existingClaim`                       | Use an existing claim to store repository information                                                 | `""`                |
| `persistence.size`                                | Size for persistence to store repo information                                                        | `10Gi`              |
| `persistence.accessModes`                         | AccessMode for persistence                                                                            | `["ReadWriteOnce"]` |
| `persistence.labels`                              | Labels for the persistence volume claim to be created                                                 | `{}`                |
| `persistence.annotations.helm.sh/resource-policy` | Resource policy for the persistence volume claim                                                      | `keep`              |
| `persistence.storageClass`                        | Name of the storage class to use                                                                      | `""`                |
| `persistence.subPath`                             | Subdirectory of the volume to mount at                                                                | `""`                |
| `persistence.mountPath`                           | Directory of the container to mount at                                                                | `/data`             |
| `persistence.volumeName`                          | Name of persistent volume in PVC                                                                      | `""`                |
| `cache`                                           | Volume for cache                                                                                      |                     |
| `cache.mountPath`                                 | Directory of the container to mount at                                                                | `/cache`            |
| `extraVolumes`                                    | Additional volumes to mount to the Gitea deployment                                                   | `[]`                |
| `extraContainerVolumeMounts`                      | Mounts that are only mapped into the Gitea runtime/main container, to e.g. override custom templates. | `[]`                |

### Miscellaneous

| Name           | Description                            | Value |
| -------------- | -------------------------------------- | ----- |
| `extraObjects` | Array of extra K8s manifests to deploy | `[]`  |
