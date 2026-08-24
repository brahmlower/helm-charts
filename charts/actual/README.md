
# actual
Helm chart for managing [Actual](https://www.actualbudget.com/)

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| replicaCount | number | `1` |  |
| image.repository | string | `"docker.io/actualbudget/actual-server"` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.tag | string | `"latest"` | Overrides the image tag whose default is the chart appVersion. |
| imagePullSecrets | array | `null` |  |
| nameOverride | string | `""` |  |
| fullnameOverride | string | `""` |  |
| serviceAccount.create | boolean | `true` | Specifies whether a service account should be created |
| serviceAccount.automount | boolean | `true` | Automatically mount a ServiceAccount's API credentials? |
| serviceAccount.name | string | `""` | The name of the service account to use.</br>If not set and create is true, a name is generated using the fullname template |
| service.type | string | `"ClusterIP"` |  |
| service.port | number | `80` |  |
| env | array | `null` |  |
| ingress.enabled | boolean | `false` |  |
| ingress.className | string | `"nginx"` |  |
| ingress.annotations.kubernetes.io/ingress.class | string | `"nginx"` |  |
| ingress.annotations.kubernetes.io/tls-acme | string | `"true"` |  |
| ingress.hosts | array | `null` |  |
| livenessProbe.httpGet.path | string | `"/"` |  |
| livenessProbe.httpGet.port | number | `5006` |  |
| readinessProbe.httpGet.path | string | `"/"` |  |
| readinessProbe.httpGet.port | number | `5006` |  |
| autoscaling.enabled | boolean | `false` |  |
| autoscaling.minReplicas | number | `1` |  |
| autoscaling.maxReplicas | number | `2` |  |
| autoscaling.targetCPUUtilizationPercentage | number | `80` |  |
| tolerations | array | `null` |  |
| persistence.data.persistentVolumeClaim | string | `"actual-data"` |  |