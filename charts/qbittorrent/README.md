
# qbittorrent
A Helm chart for Kubernetes

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| replicaCount | integer | `1` | This will set the replicaset count more information can be found here: https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/ |
| imagePullSecrets | array | `null` | This is for the secrets for pulling an image from a private repository more information can be found here: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/ |
| nameOverride | string | `""` | This is to override the chart name. |
| fullnameOverride | string | `""` | Overrides the full name of the release used to generate resource names. |
| serviceAccount.create | boolean | `true` | Specifies whether a service account should be created |
| serviceAccount.automount | boolean | `true` | Automatically mount a ServiceAccount's API credentials? |
| serviceAccount.name | string | `""` | The name of the service account to use.</br>If not set and create is true, a name is generated using the fullname template |
| service.type | string (enum)</br>"ClusterIP", "NodePort", "LoadBalancer", "ExternalName" | `"ClusterIP"` | The type of Kubernetes Service to create. |
| ingress.enabled | boolean | `false` | Whether to create an Ingress resource for the qBittorrent WebUI. |
| ingress.className | string | `""` | The IngressClass to use for the Ingress resource. |
| ingress.hosts | array | `null` | A list of host rules used to configure the Ingress. |
| ingress.tls | array | `null` | TLS configuration for the Ingress, specifying secrets and the hosts they cover. |
| autoscaling.enabled | boolean | `false` | Whether to create a HorizontalPodAutoscaler for this workload. |
| autoscaling.minReplicas | integer | `1` | The minimum number of replicas to scale down to. |
| autoscaling.maxReplicas | integer | `100` | The maximum number of replicas to scale up to. |
| autoscaling.targetCPUUtilizationPercentage | integer | `80` | Target average CPU utilization percentage used by the autoscaler. |
| volumes | array | `null` | Additional volumes on the output Deployment definition. |
| volumeMounts | array | `null` | Additional volumeMounts on the output Deployment definition. |
| tolerations | array | `null` | Tolerations allowing the pod to be scheduled onto nodes with matching taints. |
| terminationGracePeriodSeconds | integer | `15` | The number of seconds to wait for the pod to terminate gracefully, allowing the VPN tunnel and qBittorrent to shut down cleanly. |
| qbittorrent.image | string | `"lscr.io/linuxserver/qbittorrent:latest"` | linuxserver based image required to bind interface to the gluetun tunnel |
| qbittorrent.imagePullPolicy | string (enum)</br>"Always", "IfNotPresent", "Never" | `"IfNotPresent"` | The image pull policy controlling when Kubernetes re-pulls the qBittorrent image. |
| qbittorrent.config.puid | integer | `1000` | The user ID (PUID) that the qBittorrent process runs as, used to match ownership of mounted volumes. |
| qbittorrent.config.pgid | integer | `1000` | The group ID (PGID) that the qBittorrent process runs as, used to match ownership of mounted volumes. |
| qbittorrent.config.timezone | string | `"Etc/UTC"` | The timezone the qBittorrent container uses for logging and scheduling. |
| qbittorrent.config.webui_port | integer | `8080` | The port qBittorrent's WebUI listens on, used for the container port, Service, and readiness probe. |
| qbittorrent.config.torrent_port | integer | `6881` | The TCP/UDP port qBittorrent uses for BitTorrent traffic, also opened through Gluetun's firewall and used for VPN port forwarding. |
| gluetun.image | string | `"qmcgaw/gluetun:latest"` | The container image to use for the Gluetun VPN sidecar. |
| gluetun.imagePullPolicy | string (enum)</br>"Always", "IfNotPresent", "Never" | `"IfNotPresent"` | The image pull policy controlling when Kubernetes re-pulls the Gluetun image. |
| gluetun.config.puid | integer | `1000` | The user ID (PUID) that the Gluetun process runs as. |
| gluetun.config.pgid | integer | `1000` | The group ID (PGID) that the Gluetun process runs as. |
| gluetun.config.vpn_service_provider | string | `"protonvpn"` | The VPN service provider Gluetun connects through. See the Gluetun wiki for the list of supported providers. |
| gluetun.config.vpn_type | string (enum)</br>"wireguard", "openvpn" | `"wireguard"` | The VPN protocol Gluetun uses to establish the tunnel. |
| gluetun.config.wireguard_private_key | string | `""` | wireguard specific settings |
| gluetun.config.wireguard_private_key_existing_secret | string | `""` | wireguard_private_key_existing_secret names a pre-existing Secret holding</br>the wireguard private key, for use instead of the plaintext</br>wireguard_private_key value above. Takes precedence when set. |
| gluetun.config.wireguard_private_key_existing_secret_key | string | `"private_key"` | wireguard_private_key_existing_secret_key is the key within</br>wireguard_private_key_existing_secret that holds the private key. |
| gluetun.config.wireguard_address | string | `""` | The WireGuard interface address(es) (with CIDR suffix) assigned to this client by the VPN provider. |
| gluetun.config.wireguard_mtu | string | `""` | The MTU to use for the WireGuard interface. Leave empty to use Gluetun's default. |
| gluetun.config.firewall_input_ports | string | `"8080,6881"` | Allow inbound to qBittorrent through Gluetun's firewall |
| gluetun.config.firewall_outbound_subnets | string | `"10.0.0.0/8,172.16.0.0/12,192.168.0.0/16,100.64.0.0/10"` | Allow cluster/LAN subnets outbound (DNS, updates) without leaking public traffic |
| gluetun.config.dns_keep_nameserver | string | `"off"` | DNS Configuration |
| gluetun.config.dns_address | string | `"127.0.0.1"` | The IP address Gluetun's internal DNS-over-TLS resolver listens on inside the container. |
| gluetun.config.update_period | string | `"0"` | Disable problematic external checks |
| gluetun.config.version_information | string (enum)</br>"true", "false" | `"false"` | Whether Gluetun checks for and logs a newer version being available. Disabled here to avoid unnecessary external requests. |
| gluetun.config.dns_block_malicious | string | `"true"` | DNS Block List Configuration - Disable if causing issues |
| gluetun.config.dns_block_surveillance | string (enum)</br>"true", "false" | `"true"` | Whether Gluetun's DNS blocklist blocks known surveillance/tracking domains. |
| gluetun.config.dns_block_ads | string (enum)</br>"true", "false" | `"false"` | Whether Gluetun's DNS blocklist blocks known advertising domains. |
| gluetun.config.vpn_port_forwarding.enabled | boolean | `false` | Whether to enable VPN provider port forwarding. |
| gluetun.config.vpn_port_forwarding.provider | string | `"protonvpn"` | The VPN service provider to request port forwarding from. Should match vpn_service_provider. |
| gluetun.config.vpn_port_forwarding.status_file | string | `"/tmp/gluetun/forwarded_port"` | The path inside the Gluetun container where the forwarded port number is written. |
| persistence.configs.storageClassName | string | `""` | The StorageClass to use for the configs PersistentVolumeClaim. Leave empty to use the cluster default. |
| persistence.configs.size | string | `"1Gi"` | The requested size of the configs PersistentVolumeClaim. |
| persistence.downloads.storageClassName | string | `""` | The StorageClass to use for the downloads PersistentVolumeClaim. Leave empty to use the cluster default. |
| persistence.downloads.size | string | `"100Gi"` | The requested size of the downloads PersistentVolumeClaim. |