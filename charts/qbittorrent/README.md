
# qbittorrent
A Helm chart for Kubernetes

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| replicaCount | number | `1` |  |
| imagePullSecrets | array | `null` |  |
| nameOverride | string | `""` | This is to override the chart name. |
| fullnameOverride | string | `""` |  |
| serviceAccount.create | boolean | `true` | Specifies whether a service account should be created |
| serviceAccount.automount | boolean | `true` | Automatically mount a ServiceAccount's API credentials? |
| serviceAccount.name | string | `""` | The name of the service account to use.</br>If not set and create is true, a name is generated using the fullname template |
| service.type | string | `"ClusterIP"` |  |
| ingress.enabled | boolean | `false` |  |
| ingress.className | string | `""` |  |
| ingress.hosts | array | `null` |  |
| ingress.tls | array | `null` |  |
| autoscaling.enabled | boolean | `false` |  |
| autoscaling.minReplicas | number | `1` |  |
| autoscaling.maxReplicas | number | `100` |  |
| autoscaling.targetCPUUtilizationPercentage | number | `80` |  |
| volumes | array | `null` | Additional volumes on the output Deployment definition. |
| volumeMounts | array | `null` | Additional volumeMounts on the output Deployment definition. |
| tolerations | array | `null` |  |
| terminationGracePeriodSeconds | number | `15` |  |
| qbittorrent.image | string | `"lscr.io/linuxserver/qbittorrent:latest"` | linuxserver based image required to bind interface to the gluetun tunnel |
| qbittorrent.imagePullPolicy | string | `"IfNotPresent"` |  |
| qbittorrent.config.puid | number | `1000` |  |
| qbittorrent.config.pgid | number | `1000` |  |
| qbittorrent.config.timezone | string | `"Etc/UTC"` |  |
| qbittorrent.config.webui_port | number | `8080` |  |
| qbittorrent.config.torrent_port | number | `6881` |  |
| gluetun.image | string | `"qmcgaw/gluetun:latest"` |  |
| gluetun.imagePullPolicy | string | `"IfNotPresent"` |  |
| gluetun.config.puid | number | `1000` |  |
| gluetun.config.pgid | number | `1000` |  |
| gluetun.config.vpn_service_provider | string | `"protonvpn"` |  |
| gluetun.config.vpn_type | string | `"wireguard"` |  |
| gluetun.config.wireguard_private_key | string | `""` | wireguard specific settings |
| gluetun.config.wireguardPrivateKeyExistingSecret | string | `""` | wireguardPrivateKeyExistingSecret names a pre-existing Secret holding the</br>wireguard private key, for use instead of the plaintext</br>wireguard_private_key value above. Takes precedence when set. |
| gluetun.config.wireguardPrivateKeyExistingSecretKey | string | `"private_key"` | wireguardPrivateKeyExistingSecretKey is the key within</br>wireguardPrivateKeyExistingSecret that holds the private key. |
| gluetun.config.wireguard_address | string | `""` |  |
| gluetun.config.wireguard_mtu | string | `""` |  |
| gluetun.config.firewall_input_ports | string | `"8080,6881"` | Allow inbound to qBittorrent through Gluetun's firewall |
| gluetun.config.firewall_outbound_subnets | string | `"10.0.0.0/8,172.16.0.0/12,192.168.0.0/16,100.64.0.0/10"` | Allow cluster/LAN subnets outbound (DNS, updates) without leaking public traffic |
| gluetun.config.dns_keep_nameserver | string | `"off"` | DNS Configuration |
| gluetun.config.dns_address | string | `"127.0.0.1"` |  |
| gluetun.config.update_period | string | `"0"` | Disable problematic external checks |
| gluetun.config.version_information | string | `"false"` |  |
| gluetun.config.dns_block_malicious | string | `"true"` | DNS Block List Configuration - Disable if causing issues |
| gluetun.config.dns_block_surveillance | string | `"true"` |  |
| gluetun.config.dns_block_ads | string | `"false"` |  |
| gluetun.config.vpn_port_forwarding.enabled | boolean | `false` |  |
| gluetun.config.vpn_port_forwarding.provider | string | `"protonvpn"` |  |
| gluetun.config.vpn_port_forwarding.status_file | string | `"/tmp/gluetun/forwarded_port"` |  |
| persistence.configs.storageClassName | string | `""` |  |
| persistence.configs.size | string | `"1Gi"` |  |
| persistence.downloads.storageClassName | string | `""` |  |
| persistence.downloads.size | string | `"100Gi"` |  |