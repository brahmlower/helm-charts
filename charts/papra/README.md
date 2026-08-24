
# papra
A Helm chart for Papra, a minimalistic document archiving platform

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| replicaCount | number | `1` | Papra stores its database in a single SQLite file on the app-data PVC, so this must stay</br>at 1. Scaling beyond 1 replica risks corrupting the database from concurrent writers. |
| imagePullSecrets | array | `null` |  |
| nameOverride | string | `null` | This is to override the chart name. |
| fullnameOverride | string | `null` |  |
| image.repository | string | `"ghcr.io/papra-hq/papra"` |  |
| image.tag | string | `"26.6.1-rootless"` | rootless variant runs as a non-root user; matches podSecurityContext/securityContext below. |
| image.digest | string | `null` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| serviceAccount.create | boolean | `true` | Specifies whether a service account should be created |
| serviceAccount.automount | boolean | `true` | Automatically mount a ServiceAccount's API credentials? |
| serviceAccount.name | string | `null` | The name of the service account to use.</br>If not set and create is true, a name is generated using the fullname template |
| podSecurityContext.runAsNonRoot | boolean | `true` |  |
| podSecurityContext.runAsUser | number | `1000` |  |
| podSecurityContext.runAsGroup | number | `1000` |  |
| podSecurityContext.fsGroup | number | `1000` |  |
| podSecurityContext.seccompProfile.type | string | `"RuntimeDefault"` |  |
| securityContext.allowPrivilegeEscalation | boolean | `false` |  |
| securityContext.readOnlyRootFilesystem | boolean | `false` |  |
| securityContext.capabilities.drop | array | `null` |  |
| service.type | string | `"ClusterIP"` |  |
| service.port | number | `1221` | port is the HTTP port papra listens on and the Service exposes. |
| ingress.enabled | boolean | `false` |  |
| ingress.className | string | `null` |  |
| ingress.hosts | array | `null` |  |
| ingress.tls | array | `null` |  |
| resources.requests.cpu | string | `"100m"` |  |
| resources.requests.memory | string | `"256Mi"` |  |
| resources.limits.memory | string | `"512Mi"` |  |
| tolerations | array | `null` |  |
| persistence.appData.existingClaimName | string | `null` | existingClaimName uses a pre-existing PVC instead of creating one (e.g. one bound to a</br>manually-provisioned PV). When set, storageClassName and size below are ignored. |
| persistence.appData.storageClassName | string | `null` | storageClassName is the Kubernetes storage class to use. Empty string uses the cluster default. |
| persistence.appData.size | string | `"20Gi"` | size is the PVC capacity. Ignored when existingClaimName is set. |
| config.appBaseUrl | string | `null` | appBaseUrl is the full public URL of the Papra instance (required). |
| config.auth.isRegistrationEnabled | boolean | `false` | isRegistrationEnabled controls whether new users can self-register. |
| config.auth.firstUserAsAdmin | boolean | `true` | firstUserAsAdmin promotes the first registered user to admin. |
| config.auth.ipAddressHeaders | string | `"x-forwarded-for"` | ipAddressHeaders lists headers used to determine the client IP (for reverse proxy setups). |
| config.auth.customOAuthProviders | array | `null` |  |
| config.storage.driver | string | `"filesystem"` |  |
| config.storage.s3.bucket | string | `"papra"` |  |
| config.storage.s3.region | string | `"us-east-1"` |  |
| config.storage.s3.endpoint | string | `null` | endpoint is the S3-compatible endpoint URL. Leave empty to use the default AWS endpoint. |
| config.storage.s3.forcePathStyle | boolean | `false` | forcePathStyle enables path-style S3 addressing (required for MinIO and most self-hosted S3). |
| secret.create | boolean | `false` | create controls whether the chart creates the Secret.</br>Defaults to false — provide a pre-existing Secret via secretName instead (e.g. an</br>ExternalSecret), or set create=true and supply values below only for local/dev use. |
| secret.secretName | string | `null` | secretName overrides the generated Secret name when set.</br>When create=false, this must name the pre-existing Secret to use.</br>Defaults to the chart fullname when empty. |
| secret.authSecret | string | `null` | authSecret is used when create=true. Must be at least 32 characters. |
| secret.encryptionKeyEnabled | boolean | `false` |  |
| secret.databaseEncryptionKey | string | `null` | databaseEncryptionKey is used when create=true and encryptionKeyEnabled is true. |
| s3Secret.create | boolean | `false` | create controls whether the chart creates the S3 Secret.</br>Defaults to false — provide a pre-existing Secret via secretName instead,</br>or set create=true and supply values below only for local/dev use. |
| s3Secret.secretName | string | `null` | secretName overrides the generated Secret name when set.</br>Defaults to <fullname>-s3 when empty. |
| s3Secret.accessKeyId | string | `null` |  |
| s3Secret.secretAccessKey | string | `null` |  |
| oidcSecret.create | boolean | `false` | create controls whether the chart creates the OIDC Secret.</br>Defaults to false — provide a pre-existing Secret via secretName instead,</br>or set create=true and supply values below only for local/dev use. |
| oidcSecret.secretName | string | `null` | secretName overrides the generated Secret name when set.</br>Defaults to <fullname>-oidc when empty. |
| ingestionFolder.enabled | boolean | `false` |  |
| ingestionFolder.mountPath | string | `"/app/ingestion"` | mountPath is the path inside the Papra container where the share is mounted. |
| ingestionFolder.existingClaimName | string | `null` | existingClaimName uses a pre-existing PVC instead of creating one.</br>When set, claim and volume below are ignored entirely. |
| ingestionFolder.claim.storageClassName | string | `null` |  |
| ingestionFolder.claim.accessModes | array | `null` |  |
| ingestionFolder.claim.size | string | `"10Gi"` |  |
| ingestionFolder.claim.volumeName | string | `null` | volumeName explicitly binds the PVC to a specific PV by name.</br>Leave empty for dynamic provisioning.</br>Automatically set to the chart-managed PV when volume.nfs.server is configured. |
| ingestionFolder.volume.nfs.server | string | `null` | server is the NFS server hostname or IP. Leave empty to skip PV creation. |
| ingestionFolder.volume.nfs.path | string | `null` |  |
| ingestionFolder.volume.nfs.mountOptions | array | `null` |  |
| ingestionFolder.usePolling | boolean | `true` | usePolling enables polling-based file watching instead of inotify.</br>Must be true for NFS, SMB, and other network filesystems. |
| ingestionFolder.pollingIntervalMs | number | `30000` |  |
| ingestionFolder.postProcessingStrategy | string | `"delete"` |  |