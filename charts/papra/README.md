
# papra
A Helm chart for Papra, a minimalistic document archiving platform

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| replicaCount | number | `1` | Papra stores its database in a single SQLite file on the app-data PVC, so this must stay</br>at 1. Scaling beyond 1 replica risks corrupting the database from concurrent writers. |
| imagePullSecrets | array | `null` | This is for the secrets for pulling an image from a private repository. More information can</br>be found at https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/ |
| nameOverride | string | `null` | This is to override the chart name. |
| fullnameOverride | string | `null` | Overrides the full name of the release used to generate resource names. |
| image.repository | string | `"ghcr.io/papra-hq/papra"` | The container image repository to pull the Papra image from. |
| image.tag | string | `"26.6.1-rootless"` | rootless variant runs as a non-root user; matches podSecurityContext/securityContext below. |
| image.digest | string | `null` | digest pins to an immutable image reference, overriding `tag` when set. Prepend</br>`sha256:` or omit the prefix. |
| image.pullPolicy | string (enum)</br>"Always", "IfNotPresent", "Never" | `"IfNotPresent"` | The image pull policy controlling when Kubernetes re-pulls the image. |
| serviceAccount.create | boolean | `true` | Specifies whether a service account should be created |
| serviceAccount.automount | boolean | `true` | Automatically mount a ServiceAccount's API credentials? |
| serviceAccount.name | string | `null` | The name of the service account to use.</br>If not set and create is true, a name is generated using the fullname template |
| podSecurityContext.runAsNonRoot | boolean | `true` | runAsNonRoot requires the container to run as a non-root user. |
| podSecurityContext.runAsUser | integer | `1000` | runAsUser is the UID the container process runs as. |
| podSecurityContext.runAsGroup | integer | `1000` | runAsGroup is the primary GID the container process runs as. |
| podSecurityContext.fsGroup | integer | `1000` | fsGroup is the supplemental group applied to mounted volumes (e.g. the app-data PVC). |
| podSecurityContext.seccompProfile.type | string (enum)</br>"RuntimeDefault", "Unconfined", "Localhost" | `"RuntimeDefault"` | type selects which seccomp profile to apply to the pod. |
| securityContext.allowPrivilegeEscalation | boolean | `false` | allowPrivilegeEscalation controls whether a process can gain more privileges than its parent process. |
| securityContext.readOnlyRootFilesystem | boolean | `false` | readOnlyRootFilesystem mounts the container's root filesystem as read-only. |
| securityContext.capabilities.drop | array | `null` | drop is the list of Linux capabilities to remove from the container. |
| service.type | string (enum)</br>"ClusterIP", "NodePort", "LoadBalancer", "ExternalName" | `"ClusterIP"` | The type of Kubernetes Service to create. |
| service.port | number | `1221` | port is the HTTP port papra listens on and the Service exposes. |
| ingress.enabled | boolean | `false` | Whether to create an Ingress resource for exposing Papra outside the cluster. |
| ingress.className | string | `null` | The IngressClass to use for the Ingress resource. Empty string uses the cluster default. |
| ingress.hosts | array | `null` | A list of host rules used to configure the Ingress. |
| ingress.tls | array | `null` | TLS configuration for the Ingress, specifying secrets and the hosts they cover. |
| resources.requests.cpu | string | `"100m"` | cpu is the requested CPU amount (e.g. 100m). |
| resources.requests.memory | string | `"256Mi"` | memory is the requested memory amount (e.g. 256Mi). |
| resources.limits.memory | string | `"512Mi"` | memory is the maximum memory amount the container may use (e.g. 512Mi). |
| tolerations | array | `null` | Tolerations allowing the pod to be scheduled onto nodes with matching taints. |
| persistence.appData.existingClaimName | string | `null` | existingClaimName uses a pre-existing PVC instead of creating one (e.g. one bound to a</br>manually-provisioned PV). When set, storageClassName and size below are ignored. |
| persistence.appData.storageClassName | string | `null` | storageClassName is the Kubernetes storage class to use. Empty string uses the cluster default. |
| persistence.appData.size | string | `"20Gi"` | size is the PVC capacity. Ignored when existingClaimName is set. |
| config.appBaseUrl | string | `null` | appBaseUrl is the full public URL of the Papra instance (required). |
| config.auth.isRegistrationEnabled | boolean | `false` | isRegistrationEnabled controls whether new users can self-register. |
| config.auth.firstUserAsAdmin | boolean | `true` | firstUserAsAdmin promotes the first registered user to admin. |
| config.auth.ipAddressHeaders | string | `"x-forwarded-for"` | ipAddressHeaders lists headers used to determine the client IP (for reverse proxy setups). |
| config.auth.customOAuthProviders | array | `null` | customOAuthProviders configures custom OAuth/OIDC providers (AUTH_PROVIDERS_CUSTOMS).</br>Client secrets are provided via oidcSecret/oidcExternalSecret below.</br>See the better-auth generic-oauth plugin docs for field details. |
| config.storage.driver | string (enum)</br>"filesystem", "s3" | `"filesystem"` | driver is the document storage backend. This chart only wires up filesystem and s3. |
| config.storage.s3.bucket | string | `"papra"` | bucket is the S3 bucket name used to store documents. Only used when driver=s3. |
| config.storage.s3.region | string | `"us-east-1"` | region is the AWS region of the S3 bucket. Only used when driver=s3. |
| config.storage.s3.endpoint | string | `null` | endpoint is the S3-compatible endpoint URL. Leave empty to use the default AWS endpoint. |
| config.storage.s3.forcePathStyle | boolean | `false` | forcePathStyle enables path-style S3 addressing (required for MinIO and most self-hosted S3). |
| secret.create | boolean | `false` | create controls whether the chart creates the Secret.</br>Defaults to false — provide a pre-existing Secret via secretName instead (e.g. an</br>ExternalSecret), or set create=true and supply values below only for local/dev use. |
| secret.secretName | string | `null` | secretName overrides the generated Secret name when set.</br>When create=false, this must name the pre-existing Secret to use.</br>Defaults to the chart fullname when empty. |
| secret.authSecret | string | `null` | authSecret is used when create=true. Must be at least 32 characters. |
| secret.encryptionKeyEnabled | boolean | `false` | encryptionKeyEnabled wires DATABASE_ENCRYPTION_KEY from the secret's</br>"database-encryption-key" field. Encrypts the SQLite database at rest.</br>Losing this key permanently makes the database unrecoverable. |
| secret.databaseEncryptionKey | string | `null` | databaseEncryptionKey is used when create=true and encryptionKeyEnabled is true. |
| s3Secret.create | boolean | `false` | create controls whether the chart creates the S3 Secret.</br>Defaults to false — provide a pre-existing Secret via secretName instead,</br>or set create=true and supply values below only for local/dev use. |
| s3Secret.secretName | string | `null` | secretName overrides the generated Secret name when set.</br>Defaults to <fullname>-s3 when empty. |
| s3Secret.accessKeyId | string | `null` | accessKeyId is the S3 access key ID. Used when create=true; stored in the Secret's "access-key-id" field. |
| s3Secret.secretAccessKey | string | `null` | secretAccessKey is the S3 secret access key. Used when create=true; stored in the Secret's "secret-access-key" field. |
| oidcSecret.create | boolean | `false` | create controls whether the chart creates the OIDC Secret.</br>Defaults to false — provide a pre-existing Secret via secretName instead,</br>or set create=true and supply values below only for local/dev use. |
| oidcSecret.secretName | string | `null` | secretName overrides the generated Secret name when set.</br>Defaults to <fullname>-oidc when empty. |
| ingestionFolder.enabled | boolean | `false` | enabled turns on Papra's ingestion folder feature and mounts the configured volume into the container. |
| ingestionFolder.mountPath | string | `"/app/ingestion"` | mountPath is the path inside the Papra container where the share is mounted. |
| ingestionFolder.existingClaimName | string | `null` | existingClaimName uses a pre-existing PVC instead of creating one.</br>When set, claim and volume below are ignored entirely. |
| ingestionFolder.claim.storageClassName | string | `null` | storageClassName is the Kubernetes storage class to use for the ingestion folder PVC. Empty string uses the cluster default. |
| ingestionFolder.claim.accessModes | array | `null` | accessModes are the PVC access modes to request for the ingestion folder volume. |
| ingestionFolder.claim.size | string | `"10Gi"` | size is the ingestion folder PVC capacity. Ignored when existingClaimName is set. |
| ingestionFolder.claim.volumeName | string | `null` | volumeName explicitly binds the PVC to a specific PV by name.</br>Leave empty for dynamic provisioning.</br>Automatically set to the chart-managed PV when volume.nfs.server is configured. |
| ingestionFolder.volume.nfs.server | string | `null` | server is the NFS server hostname or IP. Leave empty to skip PV creation. |
| ingestionFolder.volume.nfs.path | string | `null` | path is the exported path on the NFS server to mount. |
| ingestionFolder.volume.nfs.mountOptions | array | `null` | mountOptions are the NFS mount options applied to the PersistentVolume. |
| ingestionFolder.usePolling | boolean | `true` | usePolling enables polling-based file watching instead of inotify.</br>Must be true for NFS, SMB, and other network filesystems. |
| ingestionFolder.pollingIntervalMs | integer | `30000` | pollingIntervalMs is the interval, in milliseconds, between polling scans of the ingestion folder. Only used when usePolling is true. |
| ingestionFolder.postProcessingStrategy | string (enum)</br>"delete", "move" | `"delete"` | postProcessingStrategy controls what Papra does with a file after it has been ingested.</br></br>- `delete` removes the file from the ingestion folder.</br>- `move` moves the file to the post-processing move folder instead of deleting it. |