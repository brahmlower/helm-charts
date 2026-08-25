
# kiwix
A helm chart for [kiwix](https://kiwix.org/en/).

```
helm repo add brahmlower https://brahmlower.github.io/helm-charts
helm install kiwix brahmlower/kiwix
```


| Key | Type | Default | Description |
|-----|------|---------|-------------|
| replicaCount | integer | `1` | Number of Deployment replicas to run.</br></br>This will set the replicaset count more information can be found here: https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/ |
| image.repository | string | `"ghcr.io/kiwix/kiwix-serve"` | The image url |
| image.pullPolicy | string (enum)</br>"Always", "IfNotPresent", "Never" | `"IfNotPresent"` | This sets the pull policy for images. |
| image.tag | string | `null` | Overrides the image tag whose default is the chart appVersion. |
| imagePullSecrets | array | `null` | This is for the secrets for pulling an image from a private repository more information can be found here: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/ |
| nameOverride | string | `null` | This is to override the chart name. |
| fullnameOverride | string | `null` | This is to override the fully qualified app name used for resource names. |
| args | array | `null` | args for the kiwix command |
| serviceAccount.create | boolean | `true` | Specifies whether a service account should be created |
| serviceAccount.automount | boolean | `true` | Automatically mount a ServiceAccount's API credentials? |
| serviceAccount.name | string | `null` | The name of the service account to use.</br>If not set and create is true, a name is generated using the fullname template |
| service.type | string (enum)</br>"ClusterIP", "NodePort", "LoadBalancer", "ExternalName" | `"ClusterIP"` | The Kubernetes Service type to create. See https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types for more information. |
| service.port | integer | `80` | The port the Service listens on for the Kiwix container. See https://kubernetes.io/docs/concepts/services-networking/service/#field-spec-ports for more information. |
| ingress.enabled | boolean | `false` | Whether to create an Ingress resource for kiwix. |
| ingress.className | string | `null` | The name of the IngressClass to use for this Ingress. |
| ingress.hosts | array | `null` | List of hosts and their path rules to route to the kiwix service. |
| ingress.tls | array | `null` | TLS configuration for the Ingress, mapping secretNames to hosts. |
| livenessProbe.httpGet | [Ref](https://raw.githubusercontent.com/yannh/kubernetes-json-schema/master/v1.34.0/_definitions.json#/definitions/io.k8s.api.core.v1.Probe) | `` |  |
| readinessProbe.httpGet.path | string | `"/"` | The path to request on the HTTP server for the readiness check. |
| readinessProbe.httpGet.port | string | `"http"` | The named container port to probe for the readiness check. |
| autoscaling.enabled | boolean | `false` | Whether to create a HorizontalPodAutoscaler for kiwix. When enabled, replicaCount is ignored. |
| autoscaling.minReplicas | integer | `1` | Minimum number of replicas the HorizontalPodAutoscaler will scale down to. |
| autoscaling.maxReplicas | integer | `100` | Maximum number of replicas the HorizontalPodAutoscaler will scale up to. |
| autoscaling.targetCPUUtilizationPercentage | integer | `80` | Target average CPU utilization percentage used to trigger scaling. |
| volumes | array | `null` | Additional volumes on the output Deployment definition. |
| volumeMounts | array | `null` | Additional volumeMounts on the output Deployment definition. |
| volumeClaimTemplates | array | `null` | Additional volumeClaims to create. |
| tolerations | array | `null` | Tolerations for pod assignment. See: https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/ |