# Changelog

All notable changes to the Omnix Helm chart will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Planned
- Support for Ingress resources
- NetworkPolicy templates
- Support for initContainers and sidecars
- Job and CronJob templates

## [0.1.2] - 2026-02-11

### Changed
- **BREAKING: `ports` structure changed from map to list of objects.** Each port entry now has `name`, `port` (service port), and `targetPort` (container port). This allows the Service port (e.g., 80) to differ from the container port (e.g., 3000).
  - Old: `ports: { http: 80 }` → service port 80, container port 80, target port 80
  - New: `ports: [{ name: http, port: 80, targetPort: 3000 }]` → service port 80, container port 3000, target port 3000
- Updated `deployment.yaml` to use `targetPort` for `containerPort`.
- Updated `service.yaml` to use separate `port` and `targetPort`.

## [0.1.1] - 2026-02-11

### Fixed
- **Pod labels now include `global.labels`**: Service selector uses `global.labels` but pod template was missing them, causing "Service has no endpoints" (label mismatch). Pod template now renders both `global.labels` and `pod.labels`.

### Changed
- **Clean default `values.yaml`**: Removed all demo/example data from defaults. `ports`, `env`, `volumes`, `nodeSelector`, etc. now default to empty `{}`. This prevents Helm's deep-merge from injecting unwanted values (e.g., `grpc: 50051`, `https: 443`) when users only specify their own ports.
- Probes (`livenessProbe`, `readinessProbe`) default to `enable: false`.
- `replicaCount` defaults to `1` (was `2`).
- `serviceAccount.enable` defaults to `false`.
- `hpa.enable` and `pdb.enable` default to `false`.

## [0.1.0] - 2024-12-02

### Added
- Initial release of Omnix Helm chart
- Deployment resource with flexible configuration
- Service resource (ClusterIP, NodePort, LoadBalancer support)
- ServiceAccount with optional creation
- HorizontalPodAutoscaler (HPA) support
- PodDisruptionBudget (PDB) support
- ConfigMap and Secret management from files
- Volume mounting support
- Environment variable management (direct and from ConfigMap/Secret)
- Liveness and readiness probe configurations
- Resource requests and limits
- Security contexts (pod and container level)
- Custom labels and annotations support
- RollingUpdate and Recreate deployment strategies
- Node selector support
- Image pull secrets support
- Comprehensive README documentation
- Example values.yaml with all features demonstrated

### Features
- Universal chart for any Kubernetes application
- Production-ready configurations
- Follows Kubernetes best practices
- Flexible and customizable for various use cases

---

## Version History

- **v0.1.2** - BREAKING: ports structure supports separate service/container ports
- **v0.1.1** - Fix pod label consistency + clean defaults
- **v0.1.0** - Initial public release

[Unreleased]: https://github.com/YOUR_USERNAME/omnix-chart/compare/v0.1.2...HEAD
[0.1.2]: https://github.com/YOUR_USERNAME/omnix-chart/compare/v0.1.1...v0.1.2
[0.1.1]: https://github.com/YOUR_USERNAME/omnix-chart/compare/v0.1.0...v0.1.1
[0.1.0]: https://github.com/YOUR_USERNAME/omnix-chart/releases/tag/v0.1.0
