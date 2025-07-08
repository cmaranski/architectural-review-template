# Sample Architecture Review: Inventory Service

## Problem Statement
Current inventory system is tightly coupled to warehouse database.

## Goals
- Decouple logic from DB
- Enable external access via API

## Context Diagram
\`\`\`mermaid
graph TD
    UI --> Inventory_API
    Inventory_API --> Inventory_Service
    Inventory_Service --> PostgreSQL
\`\`\`

## Risks & Tradeoffs
- Eventual consistency vs. real-time sync

## Observability & Security
- Prometheus + Grafana
- Auth via OIDC
