# ✅ Architectural Review Checklist

Use this checklist as a baseline for reviewing proposed or existing architecture decisions. Mark each with:

- [X] Yes
- [ ] No
- [ ] N/A
    
---

## 🧱 1. Architecture Fundamentals

- [ ] Problem statement is clearly defined and scoped
- [ ] Design includes a clear context diagram (Mermaid preferred)
- [ ] Tech stack choices are justified with tradeoffs explained
- [ ] Risks and failure scenarios have been explicitly addressed

---

## 🌩️ 2. Cloud-Native Alignment

- [ ] Follows [12-Factor App](https://12factor.net/) principles
- [ ] Service is stateless (or state is externalized)
- [ ] Configuration is externalized (env vars, secrets managers)
- [ ] Containerized and suitable for Kubernetes deployment
- [ ] Infrastructure is defined as code (Terraform, Pulumi, etc.)

---

## 🔐 3. Security

- [ ] Uses secure authentication (e.g., OAuth2, OIDC, JWT)
- [ ] Applies least privilege in authorization
- [ ] Secrets are managed using vaults or secret stores (no hardcoding)
- [ ] Data is encrypted in transit (TLS) and at rest
- [ ] PII is handled in compliance with regulations (e.g., GDPR, HIPAA)
- [ ] Input is sanitized and validated at all boundaries

---

## 🔭 4. Observability

- [ ] Logs are structured and include request context (e.g., trace ID, correlation ID)
- [ ] Metrics are emitted and collected (e.g., Prometheus, GCP Monitoring)
- [ ] Distributed tracing is implemented (e.g., OpenTelemetry, Jaeger)
- [ ] Dashboards exist for key SLIs/SLOs
- [ ] Alerting thresholds and escalation paths are defined

---

## ⚙️ 5. Resilience & Scalability

- [ ] Service is horizontally scalable
- [ ] Readiness/liveness probes are defined
- [ ] Circuit breakers, retries, and timeouts are configured
- [ ] Degradation modes are documented (e.g., graceful fallback)
- [ ] Disaster recovery and backup plans are defined

---

## 🧪 6. Testing & Validation

- [ ] Unit and integration tests are defined and running in CI
- [ ] Load/performance tests are defined for expected peak usage
- [ ] Chaos testing or failure injection is planned (if relevant)
- [ ] Synthetic monitoring or smoke tests are deployed post-release

---

## 🚀 7. Delivery & Ops

- [ ] CI/CD pipeline is defined and running
- [ ] Deployment strategy is defined (blue/green, rolling, canary)
- [ ] Rollbacks are automated or easy to trigger
- [ ] Environment parity exists between dev/stage/prod
- [ ] Operational ownership is assigned (on-call, escalation contact)

---

## 📌 8. Compliance & Governance

- [ ] Design decisions are documented and stored in an ADR log
- [ ] GitHub repo is linked with clear ownership and contributing guidelines
- [ ] Licenses are correctly declared for dependencies
- [ ] Third-party service usage is tracked and reviewed

---

## 🧙‍♀️ 9. Final Reviewer Notes

Use this space for flags, comments, or a summary judgment.

