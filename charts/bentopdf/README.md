
# bentopdf
A Helm chart for Kubernetes

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| replicaCount | number | `1` |  |
| image.repository | string | `"bentopdf/bentopdf-simple"` |  |
| image.pullPolicy | string | `"IfNotPresent"` | This sets the pull policy for images. |
| image.tag | string | `null` | Overrides the image tag whose default is the chart appVersion. |
| imagePullSecrets | array | `null` |  |
| nameOverride | string | `null` | This is to override the chart name. |
| fullnameOverride | string | `null` |  |
| serviceAccount.create | boolean | `true` | Specifies whether a service account should be created. |
| serviceAccount.automount | boolean | `true` | Automatically mount a ServiceAccount's API credentials? |
| serviceAccount.name | string | `null` | The name of the service account to use.</br>If not set and create is true, a name is generated using the fullname template. |
| service.type | string | `"ClusterIP"` |  |
| service.port | number | `8080` |  |
| ingress.enabled | boolean | `false` |  |
| ingress.className | string | `null` |  |
| ingress.hosts | array | `null` |  |
| ingress.tls | array | `null` |  |
| httpRoute.enabled | boolean | `false` | HTTPRoute enabled. |
| httpRoute.parentRefs | array | `null` | Which Gateways this Route is attached to. |
| httpRoute.hostnames | array | `null` | Hostnames matching HTTP header. |
| httpRoute.rules | array | `null` | List of rules and filters applied. |
| livenessProbe.httpGet.path | string | `"/"` |  |
| livenessProbe.httpGet.port | string | `"http"` |  |
| readinessProbe.httpGet.path | string | `"/"` |  |
| readinessProbe.httpGet.port | string | `"http"` |  |
| autoscaling.enabled | boolean | `false` |  |
| autoscaling.minReplicas | number | `1` |  |
| autoscaling.maxReplicas | number | `100` |  |
| autoscaling.targetCPUUtilizationPercentage | number | `80` |  |
| volumes | array | `null` | Additional volumes on the output Deployment definition. |
| volumeMounts | array | `null` | Additional volumeMounts on the output Deployment definition. |
| tolerations | array | `null` |  |