
# bookorbit
A Helm chart for BookOrbit, a self-hosted reading space for ebooks

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| appUrl | string | `""` | appUrl is the external/public URL of the BookOrbit instance (required). Used by</br>emails and Kobo endpoints. |
| clientUrl | string | `""` | clientUrl is the CORS origin for the frontend, when served from a different domain</br>than appUrl. Defaults to appUrl when empty. |
| secretName | string | `""` | secretName names a pre-existing Secret (e.g. created by an ExternalSecret) holding</br>jwt-secret and setup-bootstrap-token, and optionally email-encryption-key /</br>migration-encryption-key. |
| database.host | string | `""` |  |
| database.port | number | `5432` |  |
| database.user | string | `""` |  |
| database.name | string | `""` |  |
| database.existingSecret | string | `""` | existingSecret names a pre-existing Secret holding the database password. |
| database.existingSecretPasswordKey | string | `"postgres-password"` | existingSecretPasswordKey is the key within existingSecret that holds the password. |
| controllers.main.type | string | `"deployment"` |  |
| controllers.main.replicas | number | `1` | BookOrbit keeps book files and app data on ReadWriteOnce PVCs, so this must</br>stay at 1. Scaling beyond 1 replica risks two pods writing the same library</br>concurrently. |
| controllers.main.strategy | string | `"Recreate"` |  |
| controllers.main.pod.securityContext.runAsNonRoot | boolean | `true` |  |
| controllers.main.pod.securityContext.runAsUser | number | `1000` |  |
| controllers.main.pod.securityContext.runAsGroup | number | `1000` |  |
| controllers.main.pod.securityContext.fsGroup | number | `1000` |  |
| controllers.main.pod.securityContext.seccompProfile.type | string | `"RuntimeDefault"` |  |
| controllers.main.containers.main.image.repository | string | `"ghcr.io/bookorbit/bookorbit"` |  |
| controllers.main.containers.main.image.tag | string | `"2.7.0"` | Unlike `helm create`-based charts, app-template does not fall back to</br>Chart.appVersion automatically — the tag must be set explicitly. |
| controllers.main.containers.main.image.pullPolicy | string | `"IfNotPresent"` |  |
| controllers.main.containers.main.securityContext.allowPrivilegeEscalation | boolean | `false` |  |
| controllers.main.containers.main.securityContext.readOnlyRootFilesystem | boolean | `false` |  |
| controllers.main.containers.main.securityContext.capabilities.drop | array | `null` |  |
| controllers.main.containers.main.env.PORT | string | `"3000"` |  |
| controllers.main.containers.main.env.APP_URL | string | `"{{ .Values.appUrl }}"` |  |
| controllers.main.containers.main.env.CLIENT_URL | string | `"{{ .Values.clientUrl \| default .Values.appUrl }}"` |  |
| controllers.main.containers.main.env.NODE_MAX_OLD_SPACE_SIZE | string | `"auto"` |  |
| controllers.main.containers.main.env.BOOKORBIT_FIX_PERMISSIONS | string | `"true"` |  |
| controllers.main.containers.main.env.OIDC_ALLOW_LOCAL_ISSUERS | string | `"false"` |  |
| controllers.main.containers.main.env.CSP_ALLOW_CLOUDFLARE_INSIGHTS | string | `"false"` |  |
| controllers.main.containers.main.env.POSTGRES_HOST | string | `"{{ .Values.database.host }}"` |  |
| controllers.main.containers.main.env.POSTGRES_PORT | string | `"{{ .Values.database.port }}"` |  |
| controllers.main.containers.main.env.POSTGRES_USER | string | `"{{ .Values.database.user }}"` |  |
| controllers.main.containers.main.env.POSTGRES_DB | string | `"{{ .Values.database.name }}"` |  |
| controllers.main.containers.main.env.JWT_SECRET.valueFrom.secretKeyRef.name | string | `"{{ .Values.secretName }}"` |  |
| controllers.main.containers.main.env.JWT_SECRET.valueFrom.secretKeyRef.key | string | `"jwt-secret"` |  |
| controllers.main.containers.main.env.SETUP_BOOTSTRAP_TOKEN.valueFrom.secretKeyRef.name | string | `"{{ .Values.secretName }}"` |  |
| controllers.main.containers.main.env.SETUP_BOOTSTRAP_TOKEN.valueFrom.secretKeyRef.key | string | `"setup-bootstrap-token"` |  |
| controllers.main.containers.main.env.POSTGRES_PASSWORD.valueFrom.secretKeyRef.name | string | `"{{ .Values.database.existingSecret }}"` |  |
| controllers.main.containers.main.env.POSTGRES_PASSWORD.valueFrom.secretKeyRef.key | string | `"{{ .Values.database.existingSecretPasswordKey }}"` |  |
| controllers.main.containers.main.env.EMAIL_ENCRYPTION_KEY.valueFrom.secretKeyRef.name | string | `"{{ .Values.secretName }}"` |  |
| controllers.main.containers.main.env.EMAIL_ENCRYPTION_KEY.valueFrom.secretKeyRef.key | string | `"email-encryption-key"` |  |
| controllers.main.containers.main.env.EMAIL_ENCRYPTION_KEY.valueFrom.secretKeyRef.optional | boolean | `true` |  |
| controllers.main.containers.main.env.MIGRATION_ENCRYPTION_KEY.valueFrom.secretKeyRef.name | string | `"{{ .Values.secretName }}"` |  |
| controllers.main.containers.main.env.MIGRATION_ENCRYPTION_KEY.valueFrom.secretKeyRef.key | string | `"migration-encryption-key"` |  |
| controllers.main.containers.main.env.MIGRATION_ENCRYPTION_KEY.valueFrom.secretKeyRef.optional | boolean | `true` |  |
| controllers.main.containers.main.probes.liveness.enabled | boolean | `true` |  |
| controllers.main.containers.main.probes.liveness.type | string | `"HTTP"` |  |
| controllers.main.containers.main.probes.liveness.path | string | `"/api/v1/health"` |  |
| controllers.main.containers.main.probes.readiness.enabled | boolean | `true` |  |
| controllers.main.containers.main.probes.readiness.type | string | `"HTTP"` |  |
| controllers.main.containers.main.probes.readiness.path | string | `"/api/v1/health"` |  |
| controllers.main.containers.main.resources.requests.cpu | string | `"250m"` |  |
| controllers.main.containers.main.resources.requests.memory | string | `"512Mi"` |  |
| controllers.main.containers.main.resources.limits.memory | string | `"2Gi"` |  |
| service.main.controller | string | `"main"` |  |
| service.main.ports.http.primary | boolean | `true` |  |
| service.main.ports.http.port | number | `3000` |  |
| ingress.main.enabled | boolean | `false` |  |
| ingress.main.className | string | `""` |  |
| ingress.main.hosts | array | `null` |  |
| ingress.main.tls | array | `null` |  |
| route.main.enabled | boolean | `false` |  |
| route.main.kind | string | `"HTTPRoute"` |  |
| route.main.hostnames | array | `null` |  |
| route.main.parentRefs | array | `null` |  |
| persistence.data.type | string | `"persistentVolumeClaim"` |  |
| persistence.data.existingClaim | string | `""` |  |
| persistence.data.storageClass | string | `""` |  |
| persistence.data.accessMode | string | `"ReadWriteOnce"` |  |
| persistence.data.size | string | `"5Gi"` |  |
| persistence.data.forceRename | string | `""` | forceRename pins the PVC to a specific name instead of the chart's</br>auto-derived one. Needed when other persistence entries are added/removed,</br>since that shifts the auto-derived name and Helm would otherwise delete and</br>recreate the PVC under the new name (PVC names are immutable). |
| persistence.data.globalMounts | array | `null` |  |
| persistence.books.type | string | `"persistentVolumeClaim"` |  |
| persistence.books.existingClaim | string | `""` |  |
| persistence.books.storageClass | string | `""` |  |
| persistence.books.accessMode | string | `"ReadWriteOnce"` |  |
| persistence.books.size | string | `"50Gi"` |  |
| persistence.books.forceRename | string | `""` |  |
| persistence.books.globalMounts | array | `null` |  |