
# donetick
A Helm chart for donetick

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| replicaCount | integer | `1` | This will set the replicaset count more information can be found here: https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/ |
| image.repository | string | `"donetick/donetick"` | The container image repository to pull the donetick image from. |
| image.pullPolicy | string | `"IfNotPresent"` | This sets the pull policy for images. |
| image.tag | string | `null` | Overrides the image tag whose default is the chart appVersion. |
| imagePullSecrets | array | `null` | This is for the secrets for pulling an image from a private repository more information can be found here: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/ |
| nameOverride | string | `null` | This is to override the chart name. |
| fullnameOverride | string | `null` | Overrides the fully qualified name of the release used to generate resource names. |
| env | array | `null` | environment variables on the container |
| config.name | string | `"selfhosted"` | The display name of this Donetick instance, and also the filename used for the rendered config (config.name.yaml). |
| config.is_done_tick_dot_com | boolean | `false` | Marks this instance as the official donetick.com hosted service. Should remain false for self-hosted deployments. |
| config.is_user_creation_disabled | boolean | `false` | When true, disables the ability for new users to sign up/register accounts. |
| config.telegram.token | string | `null` | The Telegram bot API token used to send notifications.</br></br>The DT_TELEGRAM_TOKEN environment variable should be used instead of this field. |
| config.pushover.token | string | `null` | The Pushover application API token used to send notifications.</br></br>The DT_PUSHOVER_TOKEN environment variable should be used instead of this field. |
| config.database.type | string (enum)</br>"sqlite", "postgres" | `"sqlite"` | Which database backend Donetick connects to.</br></br>When set to `sqlite`, the host/port/user/password fields below are ignored. |
| config.database.migration | boolean | `true` | Whether to automatically run database schema migrations on startup. |
| config.database.host | string | `"donetick-cnpg.default.svc.cluster.local"` | Hostname of the database server. Not used when type is sqlite. |
| config.database.port | integer | `5432` | Port of the database server. Not used when type is sqlite. |
| config.database.user | string | `"donetick"` | Username used to authenticate with the database. Not used when type is sqlite. |
| config.database.password | string | `null` | The DT_DATABASE_PASSWORD environment variable should be used instead of this field. |
| config.database.name | string | `"donetick"` | Name of the database to connect to (or the sqlite database file name). |
| config.jwt.secret | string | `null` | The DT_JWT_SECRET environment variable should be used instead of this field. |
| config.jwt.session_time | string | `"168h"` | How long an issued session token remains valid before requiring the user to log in again.</br></br>Expressed as a Go duration string (e.g. `168h`). |
| config.jwt.max_refresh | string | `"168h"` | The maximum amount of time a session can be refreshed/extended before the user must re-authenticate.</br></br>Expressed as a Go duration string (e.g. `168h`). |
| config.server.port | integer | `2021` | The TCP port the Donetick HTTP server listens on inside the container. |
| config.server.read_timeout | string | `"10s"` | Maximum duration for reading the entire request, expressed as a Go duration string. |
| config.server.write_timeout | string | `"10s"` | Maximum duration before timing out writes of the response, expressed as a Go duration string. |
| config.server.rate_period | string | `"60s"` | The time window over which server.rate_limit is enforced, expressed as a Go duration string. |
| config.server.rate_limit | integer | `300` | Maximum number of requests allowed per client within server.rate_period. |
| config.server.cors_allow_origins | array | `null` | List of origins allowed to make cross-origin (CORS) requests to the API. |
| config.server.serve_frontend | boolean | `true` | Whether the server also serves the built frontend web assets, in addition to the API. |
| config.logging.level | string (enum)</br>"debug", "info", "warn", "error" | `"info"` | The minimum log level that will be emitted. |
| config.logging.encoding | string (enum)</br>"json", "console" | `"json"` | The log output format. |
| config.logging.development | boolean | `false` | Enables development-friendly logging (more verbose, human-readable output). |
| config.scheduler_jobs.due_job | string | `"30m"` | How often the job that checks for tasks that just became due runs. |
| config.scheduler_jobs.overdue_job | string | `"3h"` | How often the job that checks for overdue tasks runs. |
| config.scheduler_jobs.pre_due_job | string | `"3h"` | How often the job that checks for tasks that are about to become due runs. |
| config.email.host | string | `null` | Hostname of the SMTP server used to send emails. Leave empty to disable email sending. |
| config.email.port | integer | `0` | Port of the SMTP server used to send emails. |
| config.email.key | string | `null` | The DT_EMAIL_KEY environment variable should be used instead of this field. |
| config.email.email | string | `null` | The "from" email address used when sending emails. |
| config.email.appHost | string | `null` | The public base URL of this Donetick instance, used to build links included in outgoing emails. |
| config.oauth2.client_id | string | `null` | The OAuth2 client ID issued by the identity provider. |
| config.oauth2.client_secret | string | `null` | The DT_OAUTH2_CLIENT_SECRET environment variable should be used instead of this field. |
| config.oauth2.auth_url | string | `null` | The identity provider's authorization endpoint URL. |
| config.oauth2.token_url | string | `null` | The identity provider's token exchange endpoint URL. |
| config.oauth2.user_info_url | string | `null` | The identity provider's user info endpoint URL, used to fetch profile details after authentication. |
| config.oauth2.redirect_url | string | `null` | The URL the identity provider redirects back to after authentication, must match the provider's app configuration. |
| config.oauth2.name | string | `null` | Display name for the OAuth2 provider, shown on the login button in the UI. |
| config.realtime.enabled | boolean | `true` | Enables the real-time update feature (WebSocket/SSE push updates to connected clients). |
| config.realtime.sse_enabled | boolean | `true` | Enables Server-Sent Events (SSE) as a transport for real-time updates, in addition to WebSockets. |
| config.realtime.heartbeat_interval | string | `"60s"` | How often the server sends a heartbeat/ping to connected real-time clients, expressed as a Go duration string. |
| config.realtime.connection_timeout | string | `"120s"` | How long a real-time connection may remain idle before being closed, expressed as a Go duration string. |
| config.realtime.max_connections | integer | `1000` | Maximum number of concurrent real-time connections allowed across all users. |
| config.realtime.max_connections_per_user | integer | `5` | Maximum number of concurrent real-time connections allowed per individual user. |
| config.realtime.event_queue_size | integer | `2048` | Size of the internal queue used to buffer outgoing real-time events before they are delivered to clients. |
| config.realtime.cleanup_interval | string | `"2m"` | How often the server scans for and removes stale/dead real-time connections, expressed as a Go duration string. |
| config.realtime.stale_threshold | string | `"5m"` | How long a real-time connection may go without activity before being considered stale, expressed as a Go duration string. |
| config.realtime.enable_compression | boolean | `true` | Enables compression of real-time messages sent to clients. |
| config.realtime.enable_stats | boolean | `true` | Enables collection of real-time connection statistics/metrics. |
| config.realtime.allowed_origins | array | `null` | List of origins allowed to open real-time (WebSocket/SSE) connections.</br></br>`"*"` allows any origin. |
| serviceAccount.create | boolean | `true` | Specifies whether a service account should be created. |
| serviceAccount.automount | boolean | `true` | Automatically mount a ServiceAccount's API credentials? |
| serviceAccount.name | string | `null` | The name of the service account to use.</br>If not set and create is true, a name is generated using the fullname template. |
| securityContext | [Ref](https://raw.githubusercontent.com/instrumenta/kubernetes-json-schema/refs/heads/master/v1.18.1/_definitions.json#/definitions/io.k8s.api.core.v1.SecurityContext) | `` |  |
| service.type | string (enum)</br>"ClusterIP", "NodePort", "LoadBalancer", "ExternalName" | `"ClusterIP"` | This sets the service type more information can be found here: https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types |
| service.port | integer | `80` | This sets the ports more information can be found here: https://kubernetes.io/docs/concepts/services-networking/service/#field-spec-ports |
| ingress.enabled | boolean | `false` | Whether to create an Ingress resource for the application. |
| ingress.className | string | `null` | The name of the IngressClass to use for the Ingress resource. |
| ingress.hosts | array | `null` | List of hostnames and path rules to route to the application. |
| ingress.tls | array | `null` | TLS configuration for the Ingress resource. |
| httpRoute.enabled | boolean | `false` | HTTPRoute enabled. |
| httpRoute.parentRefs | array | `null` | Which Gateways this Route is attached to. |
| httpRoute.hostnames | array | `null` | Hostnames matching HTTP header. |
| httpRoute.rules | array | `null` | List of rules and filters applied. |
| autoscaling.enabled | boolean | `false` | Whether to create a HorizontalPodAutoscaler for the deployment. |
| autoscaling.minReplicas | integer | `1` | The minimum number of replicas the HorizontalPodAutoscaler will scale down to. |
| autoscaling.maxReplicas | integer | `100` | The maximum number of replicas the HorizontalPodAutoscaler will scale up to. |
| autoscaling.targetCPUUtilizationPercentage | integer | `80` | The average CPU utilization percentage the HorizontalPodAutoscaler targets when deciding to scale. |
| volumes | array | `null` | Additional volumes on the output Deployment definition. |
| volumeMounts | array | `null` | Additional volumeMounts on the output Deployment definition. |
| tolerations | array | `null` | A list of tolerations that allow the pod to be scheduled onto nodes with matching taints. |