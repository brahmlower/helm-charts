
# BookOrbit Helm Chart

A helm chart for [BookOrbit](https://github.com/bookorbit/bookorbit), a self-hosted reading space for ebooks.

This chart does not deploy PostgreSQL. Point `database.*` at an external instance with
the `uuid-ossp`, `pg_trgm`, and `vector` (pgvector) extensions available (e.g.
`pgvector/pgvector:pg18`).

Built on [bjw-s's `common` library chart](https://github.com/bjw-s-labs/helm-charts) —
this chart's `values.yaml` is a thin, bookorbit-specific layer over that schema
(`controllers`, `service`, `ingress`, `route`, `persistence`, `secrets`, etc.). See its
docs for anything not covered by the bookorbit-specific values documented below (e.g.
HorizontalPodAutoscaler, NetworkPolicy, ServiceMonitor).

## Installing the Chart

```
helm repo add brahmlower-bookorbit https://brahmlower.github.io/helm-bookorbit
helm install bookorbit brahmlower-bookorbit/bookorbit
```

## Contributing

### Chart Dependencies

This chart depends on bjw-s's `common` library chart. After cloning, resolve it before
linting/templating locally:
```
helm repo add bjw-s https://bjw-s-labs.github.io/helm-charts
helm dependency update charts/bookorbit
```

### Values Schema Generation

Schema generation via [helm-values](https://github.com/brahmlower/helm-values).
```
helm plugin install https://github.com/brahmlower/helm-values
```

Update the schema and docs:
```
helm values schema .
helm values docs .
```
