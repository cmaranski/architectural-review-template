# ⚙️ Shared Architectural Standards (GCP + OCP)

## Observability
- [ ] MDC or equivalent context propagation is enabled (trace ID, user ID)
- [ ] Log fields follow structured logging convention (JSON preferred)
- [ ] Each service is traceable across mesh/gateway/API logs

## Security
- [ ] Zero trust principles apply across service-to-service calls
- [ ] TLS 1.2+ required everywhere
- [ ] API access follows principle of least privilege (avoid open endpoints)
- [ ] Secret rotation policies are documented and implemented

## Documentation
- [ ] Architecture decisions logged in ADR format
- [ ] README includes:
  - Service overview
  - Dependencies
  - Contact/Owner
  - Deployment instructions
