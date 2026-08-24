
# helm-charts

A collection of Helm charts maintained by brahmlower.

## Installing

```
helm repo add brahmlower https://brahmlower.github.io/helm-charts
helm install <chart> brahmlower/<chart>
```

## Charts

| Chart | Description |
|-------|-------------|
| [actual](charts/actual) | Actual Budget |
| [bentopdf](charts/bentopdf) | BentoPDF |
| [bookorbit](charts/bookorbit) | BookOrbit, a self-hosted reading space for ebooks |
| [donetick](charts/donetick) | Donetick |
| [kiwix](charts/kiwix) | Kiwix |
| [papra](charts/papra) | Papra, a minimalistic document archiving platform |
| [qbittorrent](charts/qbittorrent) | qBittorrent (with optional Gluetun VPN sidecar) |

Each chart's `values.yaml` reference is documented in its own README, linked above.

## Contributing

This repo uses [Task](https://taskfile.dev) to lint, template, and test all charts:
```
task test
```

Individual charts can be run the same way, e.g. `task bookorbit:test`. See the root
`Taskfile.yml` for the full list of tasks.

### Values Schema Generation

Schema generation via [helm-values](https://github.com/brahmlower/helm-values).
```
helm plugin install https://github.com/brahmlower/helm-values
```

Update the schema and docs for a chart:
```
helm values schema charts/<chart>
helm values docs charts/<chart>
```
