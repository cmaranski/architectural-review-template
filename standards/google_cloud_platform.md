# ☁️ GCP Architectural Standards

## Identity & Access
- [ ] Service accounts follow least privilege
- [ ] Workload Identity Federation is preferred over long-lived keys
- [ ] IAM bindings are scoped to roles at the narrowest level (avoid `roles/editor`)

## Networking
- [ ] VPC design follows hub-and-spoke model where applicable
- [ ] Private Google Access is enabled for secure GCP service usage
- [ ] Cloud NAT is configured for egress without public IP exposure
- [ ] VPC Firewall rules are explicit and minimal

## Compute
- [ ] GKE Autopilot or Standard clusters follow naming/versioning conventions
- [ ] Cloud Functions and Cloud Run services declare memory/CPU explicitly
- [ ] Node pools are properly tainted/labeled for workload placement

## Storage
- [ ] GCS buckets enforce uniform bucket-level access
- [ ] CMEK is used where data classification requires encryption controls
- [ ] Data retention policies are defined and attached

## Observability
- [ ] Logs are sent to Cloud Logging with context labels
- [ ] Metrics are exported to Cloud Monitoring with custom dashboards for services
- [ ] Alerting policies align with SLO targets (e.g., 99.9% availability)

## Deployment
- [ ] Cloud Build pipelines are stored in version control
- [ ] Deployments are parameterized using substitutions/variables
- [ ] Build artifacts are stored in Artifact Registry with lifecycle rules
