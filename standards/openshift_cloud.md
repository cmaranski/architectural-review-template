# 🚢 OpenShift Architectural Standards

## Access & Security
- [ ] RBAC follows least privilege (avoid cluster-admin unless absolutely needed)
- [ ] Authentication is via SSO or OIDC
- [ ] Network policies are defined per namespace to enforce isolation
- [ ] Secrets are mounted from Vault or sealed-secrets, not committed in Git

## Resource Management
- [ ] All deployments declare CPU and memory requests and limits
- [ ] HPA is used where applicable for autoscaling
- [ ] Liveness and readiness probes are present and meaningful

## Networking
- [ ] Services expose only what’s needed (ClusterIP, NodePort, Route)
- [ ] Istio or OpenShift Service Mesh is used for S2S communication control
- [ ] TLS is enforced at ingress and between internal services if mesh is used

## CI/CD
- [ ] GitOps workflows via ArgoCD or Tekton are preferred
- [ ] Pipelines are versioned and stored with the application repo
- [ ] Image tags are immutable (e.g., using SHA or build ID)

## Logging & Monitoring
- [ ] Fluentd or Vector is used to route logs to centralized log stores
- [ ] Prometheus/Grafana dashboards are defined per service
- [ ] Alerts are routed through Alertmanager with escalation paths

## Compliance
- [ ] Image scanners (e.g., Trivy, Clair) are run in CI/CD
- [ ] Base images follow Red Hat UBI or hardened minimal images
- [ ] Regular vulnerability scans are tracked and remediated
