
# actual
Helm chart for managing [Actual](https://www.actualbudget.com/)

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| replicaCount | integer | `1` | The number of pod replicas to run. |
| image.repository | string | `"docker.io/actualbudget/actual-server"` | The container image repository to pull the Actual Budget server image from. |
| image.pullPolicy | string (enum)</br>"Always", "IfNotPresent", "Never" | `"IfNotPresent"` | The image pull policy controlling when Kubernetes re-pulls the image. |
| image.tag | string | `"latest"` | Overrides the image tag whose default is the chart appVersion. |
| imagePullSecrets | array | `null` | A list of secrets used for pulling the image from a private container registry. |
| nameOverride | string | `null` | Overrides the name of the chart used to generate resource names. |
| fullnameOverride | string | `null` | Overrides the full name of the release used to generate resource names. |
| serviceAccount.create | boolean | `true` | Specifies whether a service account should be created |
| serviceAccount.automount | boolean | `true` | Automatically mount a ServiceAccount's API credentials? |
| serviceAccount.name | string | `null` | The name of the service account to use.</br>If not set and create is true, a name is generated using the fullname template |
| service.type | string (enum)</br>"ClusterIP", "NodePort", "LoadBalancer", "ExternalName" | `"ClusterIP"` | The type of Kubernetes Service to create. |
| service.port | integer | `80` | The port the Service listens on. |
| env | array | `null` | A list of environment variables to set on the application container. |
| ingress.enabled | boolean | `false` | Whether to create an Ingress resource. |
| ingress.className | string | `"nginx"` | The IngressClass to use for the Ingress resource. |
| ingress.hosts | array | `null` | A list of host rules used to configure the Ingress. |
| ingress.tls | array | `null` | TLS configuration for the Ingress, specifying secrets and the hosts they cover. |
| livenessProbe.httpGet.path | string | `"/"` | The HTTP path the liveness probe requests. |
| livenessProbe.httpGet.port | integer | `5006` | The port the liveness probe connects to. |
| readinessProbe.httpGet.path | string | `"/"` | The HTTP path the readiness probe requests. |
| readinessProbe.httpGet.port | integer | `5006` | The port the readiness probe connects to. |
| autoscaling.enabled | boolean | `false` | Whether to create a HorizontalPodAutoscaler for this deployment. |
| autoscaling.minReplicas | integer | `1` | The minimum number of replicas the autoscaler will scale down to. |
| autoscaling.maxReplicas | integer | `2` | The maximum number of replicas the autoscaler will scale up to. |
| autoscaling.targetCPUUtilizationPercentage | integer | `80` | The target average CPU utilization percentage used to trigger scaling. |
| tolerations | array | `null` | Tolerations allowing the pod to be scheduled onto nodes with matching taints. |
| persistence.data.persistentVolumeClaim | string | `"actual-data"` | The name of an existing PersistentVolumeClaim to use for storing application data. |