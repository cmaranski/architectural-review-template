# 🧪 Testing and CI/CD for Legacy-to-Cloud Messaging

## ✅ Unit Tests

- Test individual transformation logic in the Strangler Service
- Validate input/output schema conformance for JSON messages

## 🔄 Integration Tests

- Use test doubles or sandbox Pub/Sub topics to simulate message publishing
- Validate end-to-end flow from Strangler → Pub/Sub → GKE → Spanner

## 🧱 Contract Testing

- Use schema validation or Pact to enforce contract between publisher and subscriber
- Ensure graceful handling of schema evolution

## 🔥 Load Testing

- Use [k6](https://k6.io/) or [Locust](https://locust.io/) for simulating high-volume input
- Validate Pub/Sub throughput and GKE autoscaling

---

## 🚀 GitOps Deployment via Argo CD & Kustomize

### 📦 Structure Overview

You follow the Platform Engineering model where:

- `base/` includes deployment YAML, default mesh policies, etc.
- `overlays/dev/`, `overlays/prod/` are Kustomize layers per environment
- Argo CD watches the `overlays/*` directory per environment

### 🧰 Kustomize Patch Example (Strangler Service)

```yaml
# overlays/dev/kustomization.yaml
resources:
  - ../../base

patchesStrategicMerge:
  - deployment-patch.yaml
  - destinationrule-patch.yaml
  - virtualservice-patch.yaml

images:
  - name: strangler-service
    newTag: "1.2.3"  # Set by Azure Pipelines
```

```yaml
# overlays/dev/deployment-patch.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: strangler-service
spec:
  template:
    spec:
      containers:
        - name: strangler-service
          resources:
            requests:
              cpu: "250m"
              memory: "256Mi"
            limits:
              cpu: "500m"
              memory: "512Mi"
```

---

## 🛡️ Service Mesh Integration (OpenShift)

The Platform Engineering team includes mesh sidecar injection by default. You may customize:

- `DestinationRule` for mTLS and outlier detection
- `VirtualService` for traffic splitting (e.g., canary deploys)
- `PeerAuthentication` and `AuthorizationPolicy` where needed

### 🧭 Observability

- **Kiali** – Use to verify live traffic flows, TLS status, service dependency graph
- **Grafana** – Auto-linked dashboards for mesh metrics (latency, RPS, error rate)
- **Prometheus** – Integrated with OpenShift Service Mesh

---

## 🔄 Pipeline Flow

1. Azure Pipelines runs tests & builds Docker image
2. Image tag (e.g., `1.2.3`) is patched into `overlays/dev/kustomization.yaml`
3. Argo CD syncs the change to OpenShift
4. Kiali + Grafana confirm mesh flow, latency, and success rates

---

## 🧠 Cleo's Notes

- Leverage `sync-waves` in Argo CD to control mesh object ordering (e.g., DestinationRule before VirtualService before Deployment)
- Use Argo CD's `jsonnet` or `ApplicationSet` generators for multi-env deployment with fewer manual overlays
- Annotate services with `sidecar.istio.io/inject: "true"` only if mesh injection isn’t global
- Coordinate with platform team for mesh-wide AuthZ policy boundaries
