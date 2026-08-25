
# bookorbit
A Helm chart for BookOrbit, a self-hosted reading space for ebooks

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| appUrl | string | `null` | appUrl is the external/public URL of the BookOrbit instance (required). Used by</br>emails and Kobo endpoints. |
| clientUrl | string | `null` | clientUrl is the CORS origin for the frontend, when served from a different domain</br>than appUrl. Defaults to appUrl when empty. |
| secretName | string | `null` | secretName names a pre-existing Secret (e.g. created by an ExternalSecret) holding</br>jwt-secret and setup-bootstrap-token, and optionally email-encryption-key /</br>migration-encryption-key. |
| database.host | string | `null` | Hostname or address of the external PostgreSQL server. |
| database.port | integer | `5432` | TCP port the external PostgreSQL server listens on. |
| database.user | string | `null` | Username BookOrbit uses to authenticate to PostgreSQL. |
| database.name | string | `null` | Name of the PostgreSQL database BookOrbit connects to. |
| database.existingSecret | string | `null` | existingSecret names a pre-existing Secret holding the database password. |
| database.existingSecretPasswordKey | string | `"postgres-password"` | existingSecretPasswordKey is the key within existingSecret that holds the password. |
| controllers.main.type | string (enum)</br>"deployment", "statefulset", "daemonset", "cronjob" | `"deployment"` | Kind of Kubernetes workload controller to render for the main controller. |
| controllers.main.replicas | number | `1` | BookOrbit keeps book files and app data on ReadWriteOnce PVCs, so this must</br>stay at 1. Scaling beyond 1 replica risks two pods writing the same library</br>concurrently. |
| controllers.main.strategy | string (enum)</br>"Recreate", "RollingUpdate" | `"Recreate"` | Deployment update strategy. Recreate is required because the RWO data/books</br>PVCs cannot be attached to two pods at once during a rolling update. |
| controllers.main.pod.securityContext.runAsNonRoot | boolean | `true` | Requires the pod's containers to run as a non-root user. |
| controllers.main.pod.securityContext.runAsUser | integer | `1000` | UID the BookOrbit container process runs as. |
| controllers.main.pod.securityContext.runAsGroup | integer | `1000` | GID the BookOrbit container process runs as. |
| controllers.main.pod.securityContext.fsGroup | integer | `1000` | GID applied to mounted volumes (data/books PVCs) so the non-root process</br>can read and write them. |
| controllers.main.pod.securityContext.seccompProfile.type | string (enum)</br>"RuntimeDefault", "Localhost", "Unconfined" | `"RuntimeDefault"` | Uses the container runtime's default seccomp profile. |
| controllers.main.containers.main.image.repository | string | `"ghcr.io/bookorbit/bookorbit"` | Container image repository for the BookOrbit application. |
| controllers.main.containers.main.image.tag | string | `"2.7.0"` | Unlike `helm create`-based charts, app-template does not fall back to</br>Chart.appVersion automatically — the tag must be set explicitly. |
| controllers.main.containers.main.image.pullPolicy | string (enum)</br>"IfNotPresent", "Always", "Never" | `"IfNotPresent"` | Kubernetes image pull policy for the BookOrbit image. |
| controllers.main.containers.main.securityContext.allowPrivilegeEscalation | boolean | `false` | Prevents the container process from gaining more privileges than its</br>parent process. |
| controllers.main.containers.main.securityContext.readOnlyRootFilesystem | boolean | `false` | Whether the container's root filesystem is mounted read-only. BookOrbit</br>needs to write outside of the data/books volumes, so this stays false. |
| controllers.main.containers.main.securityContext.capabilities.drop | array | `null` | Linux capabilities to remove from the container process. Dropping ALL</br>follows the principle of least privilege. |
| controllers.main.containers.main.env.PORT | string | `3000` | TCP port the BookOrbit server listens on inside the container. Must</br>match service.main.ports.http.port when changed. |
| controllers.main.containers.main.env.APP_URL | string | `"{{ .Values.appUrl }}"` | Public URL of the BookOrbit instance, templated from the top-level</br>appUrl value. |
| controllers.main.containers.main.env.CLIENT_URL | string | `"{{ .Values.clientUrl | default .Values.appUrl }}"` | CORS origin for the frontend, templated from the top-level clientUrl</br>value (falling back to appUrl). |
| controllers.main.containers.main.env.NODE_MAX_OLD_SPACE_SIZE | string | `"auto"` | Sets Node.js's --max-old-space-size for the BookOrbit process, in</br>megabytes. "auto" lets the application derive a value from available</br>memory. |
| controllers.main.containers.main.env.BOOKORBIT_FIX_PERMISSIONS | string (enum)</br>"true", "false" | `true` | Whether the BookOrbit entrypoint fixes ownership/permissions on its</br>data directories at startup. |
| controllers.main.containers.main.env.OIDC_ALLOW_LOCAL_ISSUERS | string (enum)</br>"true", "false" | `false` | Allows OIDC issuers that resolve to local/private network addresses.</br>Useful for self-hosted identity providers running inside the cluster</br>or LAN; leave disabled unless you need this. |
| controllers.main.containers.main.env.CSP_ALLOW_CLOUDFLARE_INSIGHTS | string (enum)</br>"true", "false" | `false` | Relaxes the Content-Security-Policy to allow loading Cloudflare</br>Insights analytics scripts. |
| controllers.main.containers.main.env.POSTGRES_HOST | string | `"{{ .Values.database.host }}"` | PostgreSQL hostname passed to BookOrbit, templated from database.host. |
| controllers.main.containers.main.env.POSTGRES_PORT | string | `"{{ .Values.database.port }}"` | PostgreSQL port passed to BookOrbit, templated from database.port. |
| controllers.main.containers.main.env.POSTGRES_USER | string | `"{{ .Values.database.user }}"` | PostgreSQL username passed to BookOrbit, templated from database.user. |
| controllers.main.containers.main.env.POSTGRES_DB | string | `"{{ .Values.database.name }}"` | PostgreSQL database name passed to BookOrbit, templated from</br>database.name. |
| controllers.main.containers.main.env.JWT_SECRET.valueFrom.secretKeyRef.name | string | `"{{ .Values.secretName }}"` | Name of the Secret holding the JWT signing secret, templated</br>from the top-level secretName value. |
| controllers.main.containers.main.env.JWT_SECRET.valueFrom.secretKeyRef.key | string | `"jwt-secret"` | Key within the Secret that holds the JWT signing secret. |
| controllers.main.containers.main.env.SETUP_BOOTSTRAP_TOKEN.valueFrom.secretKeyRef.name | string | `"{{ .Values.secretName }}"` | Name of the Secret holding the setup bootstrap token, templated</br>from the top-level secretName value. |
| controllers.main.containers.main.env.SETUP_BOOTSTRAP_TOKEN.valueFrom.secretKeyRef.key | string | `"setup-bootstrap-token"` | Key within the Secret that holds the setup bootstrap token. |
| controllers.main.containers.main.env.POSTGRES_PASSWORD.valueFrom.secretKeyRef.name | string | `"{{ .Values.database.existingSecret }}"` | Name of the Secret holding the PostgreSQL password, templated</br>from database.existingSecret. |
| controllers.main.containers.main.env.POSTGRES_PASSWORD.valueFrom.secretKeyRef.key | string | `"{{ .Values.database.existingSecretPasswordKey }}"` | Key within the Secret that holds the PostgreSQL password,</br>templated from database.existingSecretPasswordKey. |
| controllers.main.containers.main.env.EMAIL_ENCRYPTION_KEY.valueFrom.secretKeyRef.name | string | `"{{ .Values.secretName }}"` | Name of the Secret holding the email encryption key, templated</br>from the top-level secretName value. |
| controllers.main.containers.main.env.EMAIL_ENCRYPTION_KEY.valueFrom.secretKeyRef.key | string | `"email-encryption-key"` | Key within the Secret that holds the email encryption key. |
| controllers.main.containers.main.env.EMAIL_ENCRYPTION_KEY.valueFrom.secretKeyRef.optional | boolean | `true` | When true, BookOrbit starts even if this key is absent from the</br>Secret, instead of failing to schedule the pod. |
| controllers.main.containers.main.env.MIGRATION_ENCRYPTION_KEY.valueFrom.secretKeyRef.name | string | `"{{ .Values.secretName }}"` | Name of the Secret holding the migration encryption key,</br>templated from the top-level secretName value. |
| controllers.main.containers.main.env.MIGRATION_ENCRYPTION_KEY.valueFrom.secretKeyRef.key | string | `"migration-encryption-key"` | Key within the Secret that holds the migration encryption key. |
| controllers.main.containers.main.env.MIGRATION_ENCRYPTION_KEY.valueFrom.secretKeyRef.optional | boolean | `true` | When true, BookOrbit starts even if this key is absent from the</br>Secret, instead of failing to schedule the pod. |
| controllers.main.containers.main.probes.liveness.enabled | boolean | `true` | Enables the liveness probe. |
| controllers.main.containers.main.probes.liveness.type | string (enum)</br>"HTTP", "TCP", "Command", "gRPC" | `"HTTP"` | Probe mechanism used for the liveness check. |
| controllers.main.containers.main.probes.liveness.path | string | `"/api/v1/health"` | HTTP path checked for the liveness probe. |
| controllers.main.containers.main.probes.readiness.enabled | boolean | `true` | Enables the readiness probe. |
| controllers.main.containers.main.probes.readiness.type | string (enum)</br>"HTTP", "TCP", "Command", "gRPC" | `"HTTP"` | Probe mechanism used for the readiness check. |
| controllers.main.containers.main.probes.readiness.path | string | `"/api/v1/health"` | HTTP path checked for the readiness probe. |
| controllers.main.containers.main.resources.requests.cpu | string | `"250m"` | Minimum CPU guaranteed to the BookOrbit container. |
| controllers.main.containers.main.resources.requests.memory | string | `"512Mi"` | Minimum memory guaranteed to the BookOrbit container. |
| controllers.main.containers.main.resources.limits.memory | string | `"2Gi"` | Maximum memory the BookOrbit container may use before being OOM</br>killed. No CPU limit is set, so CPU usage is not throttled. |
| service.main.controller | string | `"main"` | Name of the controller this Service routes traffic to. |
| service.main.ports.http.primary | boolean | `true` | Marks this as the Service's primary port, used e.g. as the default for</br>ingress/route backends. |
| service.main.ports.http.port | integer | `3000` | Port the Service listens on and forwards to the container's PORT env</br>var. |
| ingress.main.enabled | boolean | `false` | Enables creation of the Ingress resource. |
| ingress.main.className | string | `null` | IngressClass to use. Leave empty to use the cluster's default</br>IngressClass. |
| ingress.main.hosts | array | `null` | List of hostnames (and their path routing rules) the Ingress should</br>accept traffic for. |
| ingress.main.tls | array | `null` | TLS configuration blocks for the Ingress, pairing hostnames with the</br>Secret containing their certificate. |
| route.main.enabled | boolean | `false` | Enables creation of the HTTPRoute resource. |
| route.main.kind | string (enum)</br>"HTTPRoute", "GRPCRoute", "TCPRoute", "TLSRoute", "UDPRoute" | `"HTTPRoute"` | Gateway API route kind to create. |
| route.main.hostnames | array | `null` | Hostnames the route matches incoming requests against. |
| route.main.parentRefs | array | `null` | References to the Gateway(s) this route attaches to. This chart does not</br>create the Gateway itself. |
| persistence.data.type | string (enum)</br>"persistentVolumeClaim", "emptyDir", "configMap", "secret", "nfs", "hostPath", "custom" | `"persistentVolumeClaim"` | Kind of volume source backing this persistence entry. |
| persistence.data.existingClaim | string | `null` | Name of a pre-existing PVC to use instead of letting the chart create one.</br>Leave empty to have the chart provision and manage the PVC. |
| persistence.data.storageClass | string | `null` | StorageClass requested for the PVC. Leave empty to use the cluster's</br>default StorageClass. |
| persistence.data.accessMode | string (enum)</br>"ReadWriteOnce", "ReadOnlyMany", "ReadWriteMany", "ReadWriteOncePod" | `"ReadWriteOnce"` | Access mode requested for the PVC. |
| persistence.data.size | string | `"5Gi"` | Size of the PVC to provision for BookOrbit's app data (covers, book</br>bucket, DB migration state). |
| persistence.data.forceRename | string | `null` | forceRename pins the PVC to a specific name instead of the chart's</br>auto-derived one. Needed when other persistence entries are added/removed,</br>since that shifts the auto-derived name and Helm would otherwise delete and</br>recreate the PVC under the new name (PVC names are immutable). |
| persistence.data.globalMounts | array | `null` | Paths inside the main container where this volume is mounted. |
| persistence.books.type | string (enum)</br>"persistentVolumeClaim", "emptyDir", "configMap", "secret", "nfs", "hostPath", "custom" | `"persistentVolumeClaim"` | Kind of volume source backing this persistence entry. |
| persistence.books.existingClaim | string | `null` | Name of a pre-existing PVC to use instead of letting the chart create one.</br>Leave empty to have the chart provision and manage the PVC. |
| persistence.books.storageClass | string | `null` | StorageClass requested for the PVC. Leave empty to use the cluster's</br>default StorageClass. |
| persistence.books.accessMode | string (enum)</br>"ReadWriteOnce", "ReadOnlyMany", "ReadWriteMany", "ReadWriteOncePod" | `"ReadWriteOnce"` | Access mode requested for the PVC. |
| persistence.books.size | string | `"50Gi"` | Size of the PVC to provision for BookOrbit's book library. |
| persistence.books.forceRename | string | `null` | Pins the books PVC to a specific name instead of the chart's auto-derived</br>one. See persistence.data.forceRename above for why this exists. |
| persistence.books.globalMounts | array | `null` | Paths inside the main container where this volume is mounted. |