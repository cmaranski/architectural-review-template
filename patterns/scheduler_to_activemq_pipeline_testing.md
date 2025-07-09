# 🧪 Testing and CI/CD for Scheduled DB2 → ActiveMQ Pattern

## ✅ Unit Tests

- Validate Quartz schedule triggers expected job logic
- Ensure message formatting logic handles edge cases

## 🔁 Integration Tests

- Use TestContainers to spin up DB2 and ActiveMQ in local/CI environments
- Test full round-trip from DB2 read → transformation → publish to queue

## 🧱 Schema Validation

- Use XML schema (XSD) or JSON schema to validate message structure
- Confirm legacy system deserializes properly

## 🔥 Load & Chaos Tests

- Simulate backlogs by pausing legacy system and verifying queue handling
- Introduce failure in DB2/ActiveMQ to test retries and logging

---

## 🚀 CI/CD with Azure Pipelines

- Test suite runs during pipeline execution
- Docker image build tagged by pipeline run ID
- Kustomize overlay is patched with image tag
- Argo CD watches `overlays/dev` and syncs upon tag change

```yaml
# azure-pipelines.yml (fragment)
steps:
- task: UsePythonVersion@0
  inputs:
    versionSpec: '3.11'

- script: |
    pip install -r requirements.txt
    pytest tests/
  displayName: 'Run tests'
```

---

## 🔧 GitOps & Argo CD Deployment

- Kustomize overlays include:
  - CRON schedule
  - ConfigMap for DB2 query
  - Secret mount for credentials
- Argo CD syncs updates to OpenShift scheduler pod

---

## 📊 Observability

- Logs sent to centralized logging (Fluentd, Vector)
- Job metrics exported (Prometheus): `last_run_time`, `duration_seconds`, `records_published`
- Alert on high queue depth or repeated failures
