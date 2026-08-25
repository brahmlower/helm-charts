
# bentopdf
A Helm chart for Kubernetes

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| replicaCount | integer | `1` | The number of pod replicas to run. |
| image.repository | string | `"bentopdf/bentopdf-simple"` | The container image repository to pull the bentopdf image from. |
| image.pullPolicy | string | `"IfNotPresent"` | This sets the pull policy for images. |
| image.tag | string | `null` | Overrides the image tag whose default is the chart appVersion. |
| imagePullSecrets | array | `null` | A list of secrets used for pulling the bentopdf image from a private container registry. |
| nameOverride | string | `null` | This is to override the chart name. |
| fullnameOverride | string | `null` | Overrides the fully qualified name of the release used to generate resource names. |
| serviceAccount.create | boolean | `true` | Specifies whether a service account should be created. |
| serviceAccount.automount | boolean | `true` | Automatically mount a ServiceAccount's API credentials? |
| serviceAccount.name | string | `null` | The name of the service account to use.</br>If not set and create is true, a name is generated using the fullname template. |
| service.type | string (enum)</br>"ClusterIP", "NodePort", "LoadBalancer", "ExternalName" | `"ClusterIP"` | The Kubernetes Service type used to expose bentopdf. |
| service.port | integer | `8080` | The port the bentopdf Service listens on. |
| ingress.enabled | boolean | `false` | Whether to create an Ingress resource for bentopdf. |
| ingress.className | string | `null` | The IngressClass to use for the Ingress resource. |
| ingress.hosts | array | `null` | The list of hostnames and paths routed to the bentopdf service. |
| ingress.tls | array | `null` | TLS configuration for the Ingress, mapping secret names to hostnames. |
| httpRoute.enabled | boolean | `false` | HTTPRoute enabled. |
| httpRoute.parentRefs | array | `null` | Which Gateways this Route is attached to. |
| httpRoute.hostnames | array | `null` | Hostnames matching HTTP header. |
| httpRoute.rules | array | `null` | List of rules and filters applied. |
| livenessProbe.httpGet.path | string | `"/"` | The HTTP path the liveness probe requests. |
| livenessProbe.httpGet.port | string | `"http"` | The named container port the liveness probe targets. |
| readinessProbe.httpGet.path | string | `"/"` | The HTTP path the readiness probe requests. |
| readinessProbe.httpGet.port | string | `"http"` | The named container port the readiness probe targets. |
| autoscaling.enabled | boolean | `false` | Whether to create a HorizontalPodAutoscaler for bentopdf, replacing the static replicaCount. |
| autoscaling.minReplicas | integer | `1` | The minimum number of pod replicas the autoscaler will maintain. |
| autoscaling.maxReplicas | integer | `100` | The maximum number of pod replicas the autoscaler is allowed to scale up to. |
| autoscaling.targetCPUUtilizationPercentage | integer | `80` | The target average CPU utilization percentage the autoscaler scales towards. |
| volumes | array | `null` | Additional volumes on the output Deployment definition. |
| volumeMounts | array | `null` | Additional volumeMounts on the output Deployment definition. |
| tolerations | array | `null` | Tolerations allowing the bentopdf pod to be scheduled onto nodes with matching taints. |