
# donetick
A Helm chart for donetick

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| replicaCount | number | `1` |  |
| image.repository | string | `"donetick/donetick"` |  |
| image.pullPolicy | string | `"IfNotPresent"` | This sets the pull policy for images. |
| image.tag | string | `null` | Overrides the image tag whose default is the chart appVersion. |
| imagePullSecrets | array | `null` |  |
| nameOverride | string | `null` | This is to override the chart name. |
| fullnameOverride | string | `null` |  |
| env | array | `null` | environment variables on the container |
| config.name | string | `"selfhosted"` |  |
| config.is_done_tick_dot_com | boolean | `false` |  |
| config.is_user_creation_disabled | boolean | `false` |  |
| config.telegram.token | string | `null` |  |
| config.pushover.token | string | `null` |  |
| config.database.type | string (enum)</br>"sqlite", "postgres" | `"sqlite"` |  |
| config.database.migration | boolean | `true` |  |
| config.database.host | string | `"donetick-cnpg.default.svc.cluster.local"` |  |
| config.database.port | number | `5432` |  |
| config.database.user | string | `"donetick"` |  |
| config.database.password | string | `null` | The DT_DATABASE_PASSWORD environment variable should be used instead of this field. |
| config.database.name | string | `"donetick"` |  |
| config.jwt.secret | string | `null` | The DT_JWT_SECRET environment variable should be used instead of this field. |
| config.jwt.session_time | string | `"168h"` |  |
| config.jwt.max_refresh | string | `"168h"` |  |
| config.server.port | number | `2021` |  |
| config.server.read_timeout | string | `"10s"` |  |
| config.server.write_timeout | string | `"10s"` |  |
| config.server.rate_period | string | `"60s"` |  |
| config.server.rate_limit | number | `300` |  |
| config.server.cors_allow_origins | array | `null` |  |
| config.server.serve_frontend | boolean | `true` |  |
| config.logging.level | string | `"info"` |  |
| config.logging.encoding | string | `"json"` |  |
| config.logging.development | boolean | `false` |  |
| config.scheduler_jobs.due_job | string | `"30m"` |  |
| config.scheduler_jobs.overdue_job | string | `"3h"` |  |
| config.scheduler_jobs.pre_due_job | string | `"3h"` |  |
| config.email.host | string | `null` |  |
| config.email.port | number | `0` |  |
| config.email.key | string | `null` | The DT_EMAIL_KEY environment variable should be used instead of this field. |
| config.email.email | string | `null` |  |
| config.email.appHost | string | `null` |  |
| config.oauth2.client_id | string | `null` |  |
| config.oauth2.client_secret | string | `null` | The DT_OAUTH2_CLIENT_SECRET environment variable should be used instead of this field. |
| config.oauth2.auth_url | string | `null` |  |
| config.oauth2.token_url | string | `null` |  |
| config.oauth2.user_info_url | string | `null` |  |
| config.oauth2.redirect_url | string | `null` |  |
| config.oauth2.name | string | `null` |  |
| config.realtime.enabled | boolean | `true` |  |
| config.realtime.sse_enabled | boolean | `true` |  |
| config.realtime.heartbeat_interval | string | `"60s"` |  |
| config.realtime.connection_timeout | string | `"120s"` |  |
| config.realtime.max_connections | number | `1000` |  |
| config.realtime.max_connections_per_user | number | `5` |  |
| config.realtime.event_queue_size | number | `2048` |  |
| config.realtime.cleanup_interval | string | `"2m"` |  |
| config.realtime.stale_threshold | string | `"5m"` |  |
| config.realtime.enable_compression | boolean | `true` |  |
| config.realtime.enable_stats | boolean | `true` |  |
| config.realtime.allowed_origins | array | `null` |  |
| serviceAccount.create | boolean | `true` | Specifies whether a service account should be created. |
| serviceAccount.automount | boolean | `true` | Automatically mount a ServiceAccount's API credentials? |
| serviceAccount.name | string | `null` | The name of the service account to use.</br>If not set and create is true, a name is generated using the fullname template. |
| securityContext | [Ref](https://raw.githubusercontent.com/instrumenta/kubernetes-json-schema/refs/heads/master/v1.18.1/_definitions.json#/definitions/io.k8s.api.core.v1.SecurityContext) | `` |  |
| service.type | string | `"ClusterIP"` |  |
| service.port | number | `80` |  |
| ingress.enabled | boolean | `false` |  |
| ingress.className | string | `null` |  |
| ingress.hosts | array | `null` |  |
| ingress.tls | array | `null` |  |
| httpRoute.enabled | boolean | `false` | HTTPRoute enabled. |
| httpRoute.parentRefs | array | `null` | Which Gateways this Route is attached to. |
| httpRoute.hostnames | array | `null` | Hostnames matching HTTP header. |
| httpRoute.rules | array | `null` | List of rules and filters applied. |
| autoscaling.enabled | boolean | `false` |  |
| autoscaling.minReplicas | number | `1` |  |
| autoscaling.maxReplicas | number | `100` |  |
| autoscaling.targetCPUUtilizationPercentage | number | `80` |  |
| volumes | array | `null` | Additional volumes on the output Deployment definition. |
| volumeMounts | array | `null` | Additional volumeMounts on the output Deployment definition. |
| tolerations | array | `null` |  |