# RHACM MultiClusterObservability (MCO) – S3 Backend

This repository contains YAML and helper scripts to deploy **Red Hat Advanced Cluster Management (RHACM) Observability** (`MultiClusterObservability`) on the **hub** with an **S3/S3-compatible** object storage backend (Thanos object storage).

## What this repo deploys

### Hub components (hub cluster)
- Namespace: `open-cluster-management-observability`
- `MultiClusterObservability` custom resource
- Thanos receive/query/store/compact/rule components (deployed by the operator)

### Managed cluster components (per managed cluster)
- Observability add-on (`ManagedClusterAddOn/observability-controller`)
- Metrics collector running in `open-cluster-management-addon-observability`

## Repo structure

- `manifests/`
  - `-namespace.yaml`
  - `multiclusterobservability.yaml`
- `scripts/`
  - `create-mco-pull-secret.sh` (optional helper)
  - (optional) S3 CA and Thanos secret creation scripts (recommended, not committed with secrets)
- `secrets/` (recommended locally, NOT committed)
  - `ca.crt` (S3 endpoint CA certificate)

## Prerequisites

- You have `oc` access to the RHACM hub cluster with sufficient privileges.
- A working StorageClass exists for the hub (PVC provisioning must succeed).
- S3 bucket + credentials are ready.
- CA certificate for the S3 endpoint is available (same approach used for LokiStack / etcd backup).

## Deployment steps (hub)

oc apply -k .

