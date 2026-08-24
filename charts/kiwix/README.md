
# kiwix
A helm chart for [kiwix](https://kiwix.org/en/).

```
helm repo add brahmlower-kiwix https://brahmlower.github.io/helm-kiwix
helm install kiwix brahmlower-kiwix/kiwix
```


| Key | Type | Default | Description |
|-----|------|---------|-------------|
| replicaCount | number | `1` |  |
| image.repository | string | `"ghcr.io/kiwix/kiwix-serve"` | The image url |
| image.pullPolicy | string | `"IfNotPresent"` | This sets the pull policy for images. |
| image.tag | string | `null` | Overrides the image tag whose default is the chart appVersion. |
| imagePullSecrets | array | `null` |  |
| nameOverride | string | `null` | This is to override the chart name. |
| fullnameOverride | string | `null` |  |
| args | array | `null` | args for the kiwix command |
| serviceAccount.create | boolean | `true` | Specifies whether a service account should be created |
| serviceAccount.automount | boolean | `true` | Automatically mount a ServiceAccount's API credentials? |
| serviceAccount.name | string | `null` | The name of the service account to use.</br>If not set and create is true, a name is generated using the fullname template |
| service.type | string | `"ClusterIP"` |  |
| service.port | number | `80` |  |
| ingress.enabled | boolean | `false` |  |
| ingress.className | string | `null` |  |
| ingress.hosts | array | `null` |  |
| ingress.tls | array | `null` |  |
| livenessProbe.httpGet | [Ref](https://raw.githubusercontent.com/yannh/kubernetes-json-schema/master/v1.34.0/_definitions.json#/definitions/io.k8s.api.core.v1.Probe) | `` |  |
| readinessProbe.httpGet.path | string | `"/"` |  |
| readinessProbe.httpGet.port | string | `"http"` |  |
| autoscaling.enabled | boolean | `false` |  |
| autoscaling.minReplicas | number | `1` |  |
| autoscaling.maxReplicas | number | `100` |  |
| autoscaling.targetCPUUtilizationPercentage | number | `80` |  |
| volumes | array | `null` | Additional volumes on the output Deployment definition. |
| volumeMounts | array | `null` | Additional volumeMounts on the output Deployment definition. |
| volumeClaimTemplates | array | `null` | Additional volumeClaims to create. |
| tolerations | array | `null` |  |