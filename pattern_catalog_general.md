# Merged Pattern Library
##  Patterns Summary

| PatternID | Name | Intended use case | Runtime type | When to use | 
|---|---|---|---|---|
| `PAT-001` | Batch Orchestration Pipeline | Managed workflow orchestration with structured storage, object storage, query engine, and deploy chain. | Workflow orchestration | Enterprise analytics & data lake, regulatory data storage, scheduled ETL/ELT | 
| `PAT-002` | Serverless Application  | Serverless compute with a managed relational database and supporting security/identity modules.| Serverless container runtime | Internal tooling & PoCs, lightweight public APIs, low-traffic web apps | 
| `PAT-003` | Managed Orchestration Application| Managed container orchestration with perimeter security, private networking, managed database access, and shared cluster operations for platform/SRE teams. | Managed container orchestration / Shared K8s platform runtime | Customer-facing production apps, regulatory workloads, high-SLA services; Platform/SRE teams, multi-tenant cluster hosting |
| `PAT-004` | Event-Driven Microservices Platform | Decoupled services communicating via an async messaging bus, with event routing, fast in-memory/document stores, and observability tooling. | Serverless or container runtime + message bus | Decoupled microservices, fan-out/fan-in workloads, event-sourced systems | 
| `PAT-005` | Data Ingestion Landing Zone | Ingestion and storage foundation centred on object storage, structured datasets, identity controls, and landing-zone access patterns. | Data foundation | Data lake raw zone, multi-source ingestion | 
| `PAT-006` | Specialised VM Workload Platform | VM-centric stack with network, firewall, and relational database resources for proprietary or specialised software that cannot run in containers. | Specialised virtual machine | Licensed desktop-class software, GIS/CAD platforms, legacy workloads |

### PAT-001 - Batch Orchestration Pipeline

Managed workflow orchestration with structured storage, object storage, query engine, and deploy chain.

- Status: `first_release_candidate`
- Release bucket: `released_reusable_pattern`
- First-release treatment: First-release reusable pattern candidate for architecture/security approval.
- Runtime type: `Workflow / data orchestration`
- Project count: `15`
- Required building blocks: `bastion, delivery, environment, integration, keys, network, security_operations`
- Optional building blocks: `bigquery, bucket, workflow, K8s, iam, network_policy, pubsub, security_policy, sql`
- Representative examples: `vf-de-nwp-live, vf-de-nwp-nonlive, vf-gned-nwp-live, vf-gned-nwp-nonlive, vf-gned-nwpccs-live`

Underlying Terraform module mapping:

- `bastion` -> `bastion_vm`
- `bigquery` -> `bigquery`, `bigquery_table`
- `bucket` -> `gcs`
- `composer` -> `composer_environment`
- `delivery` -> `cloud_build`, `cloud_build_private_worker_pool`
- `environment` -> *(template-level config — no GCP modules)*
- `K8s` -> `gke_autopilot_cluster`, `gke_standard_cluster`
- `iam` -> `iam_service_account`, `project_iam`, `iam_custom_role_stack`, `service_agent_iam`
- `integration` -> `vpc_connector`, `workload_identity`, `cloud_build`
- `keys` -> `kms`
- `network` -> `network`, `firewall`, `dns`, `external_global_address`, `external_global_loadbalancer`
- `network_policy` -> `firewall`, `vf_security_policy`
- `pubsub` -> `pubsub`
- `security_operations` -> `alert_policy`, `notification_channel`, `dashboard_bq`, `dashboard_composer`, `dashboard_dataproc`, `dashboard_gcs`
- `security_policy` -> `vf_security_policy`
- `sql` -> `cloud_sql`

### PAT-002 - Serverless Application 

Serverless compute with a managed relational database and supporting security/identity modules.

- Status: `first_release_candidate`
- Release bucket: `released_reusable_pattern`
- First-release treatment: First-release reusable pattern candidate for architecture/security approval.
- Runtime type: `Cloud Run`
- Project count: `5`
- Required building blocks: `bastion, bucket, serverless_app, iam, keys, network, security_operations, security_policy, sql`
- Optional building blocks: `bigquery, workflow, delivery, environment, integration, network_policy, pubsub`
- Representative examples: `vf-gned-nwpenergyedm-live, vf-gned-nwpenergyedm-nonlive, vf-gned-nwpenergyib-live, vf-gned-nwpenergyib-nonlive, vf-gned-str-nonlive`

Underlying Terraform module mapping:

- `bastion` -> `bastion_vm`
- `bigquery` -> `bigquery`, `bigquery_table`
- `bucket` -> `gcs`
- `serverless_app` -> `cloud_run`
- `composer` -> `composer_environment`
- `delivery` -> `cloud_build`, `cloud_build_private_worker_pool`
- `environment` -> *(template-level config — no GCP modules)*
- `iam` -> `iam_service_account`, `project_iam`, `iam_custom_role_stack`, `service_agent_iam`
- `integration` -> `vpc_connector`, `workload_identity`, `cloud_build`
- `keys` -> `kms`
- `network` -> `network`, `firewall`, `dns`, `external_global_address`, `external_global_loadbalancer`
- `network_policy` -> `firewall`, `vf_security_policy`
- `pubsub` -> `pubsub`
- `security_operations` -> `alert_policy`, `notification_channel`, `dashboard_bq`, `dashboard_composer`, `dashboard_dataproc`, `dashboard_gcs`
- `security_policy` -> `vf_security_policy`
- `sql` -> `cloud_sql`

### PAT-003 - Managed Orchestration Application

Managed container orchestration and shared platform runtime project. Provides perimeter security, private networking, managed database access, and supporting identity/messaging services. Also serves as central shared infrastructure for K8s clusters, worker pools, and platform-level operations for platform and SRE teams. *Merged with Shared Runtime / Platform Project (PAT-007).*

- Status: `first_release_candidate`
- Release bucket: `released_reusable_pattern`
- First-release treatment: First-release reusable pattern candidate for architecture/security approval.
- Runtime type: `K8s / Helm / Shared K8s platform runtime`
- Project count: `6`
- Required building blocks: `bastion, bigquery, bucket, composer, delivery, environment, K8s, helm, iam, integration, keys, network, security_operations, security_policy, sql`
- Optional building blocks: `network_policy, platform_operations, pubsub`
- Representative examples: `vf-gned-nwpccs-nonlive, vf-it-nwp-nonlive, vf-ro-nwp-live, vf-ro-nwp-nonlive, vf-nwp-cntr-nonlive, vf-nwp-sreapm-nonlive`

Underlying Terraform module mapping:

- `bastion` -> `bastion_vm`
- `bigquery` -> `bigquery`, `bigquery_table`
- `bucket` -> `gcs`
- `workflow` -> `composer_environment`
- `delivery` -> `cloud_build`, `cloud_build_private_worker_pool`
- `environment` -> *(template-level config — no GCP modules)*
- `K8s` -> `gke_autopilot_cluster`, `gke_standard_cluster`
- `helm` -> `gap` *(to be replaced with ArgoCD)*
- `iam` -> `iam_service_account`, `project_iam`, `iam_custom_role_stack`, `service_agent_iam`
- `integration` -> `vpc_connector`, `workload_identity`, `cloud_build`
- `keys` -> `kms`
- `network` -> `network`, `firewall`, `dns`, `external_global_address`, `external_global_loadbalancer`
- `network_policy` -> `firewall`, `vf_security_policy`
- `platform_operations` -> `cloud_build_private_worker_pool`, `workload_identity`, `project_services`
- `pubsub` -> `pubsub`
- `security_operations` -> `alert_policy`, `notification_channel`, `dashboard_bq`, `dashboard_composer`, `dashboard_dataproc`, `dashboard_gcs`
- `security_policy` -> `vf_security_policy`
- `sql` -> `cloud_sql`

### PAT-004 - Event-Driven Microservices Platform

Decoupled services communicating via an async messaging bus, with event routing, fast in-memory/document stores, and observability tooling.

- Status: `first_release_candidate`
- Release bucket: `released_reusable_pattern`
- First-release treatment: First-release reusable pattern candidate for architecture/security approval.
- Runtime type: `Serverless or container runtime + message bus`
- Project count: `?`
- Required building blocks: `iam, keys, network, pubsub, security_operations, security_policy`
- Optional building blocks: `bigquery, bucket, serverless_app, delivery, environment, K8s, helm, integration, network_policy, sql`
- Representative examples: `?`

Underlying Terraform module mapping:

- `iam` -> `iam_service_account`, `project_iam`, `iam_custom_role_stack`, `service_agent_iam`
- `keys` -> `kms`
- `network` -> `network`, `firewall`, `dns`, `external_global_address`, `external_global_loadbalancer`
- `pubsub` -> `pubsub`
- `security_operations` -> `alert_policy`, `notification_channel`, `dashboard_bq`, `dashboard_composer`, `dashboard_dataproc`, `dashboard_gcs`
- `security_policy` -> `vf_security_policy`
- `bigquery` -> `bigquery`, `bigquery_table`
- `bucket` -> `gcs`
- `serverless_app` -> `cloud_run`
- `delivery` -> `cloud_build`, `cloud_build_private_worker_pool`
- `environment` -> *(template-level config — no GCP modules)*
- `K8s` -> `gke_autopilot_cluster`, `gke_standard_cluster`
- `helm` -> `gap` *(to be replaced with ArgoCD)*
- `integration` -> `vpc_connector`, `workload_identity`, `cloud_build`
- `network_policy` -> `firewall`, `vf_security_policy`
- `sql` -> `cloud_sql`

## Candidate And Reference Patterns

These remain visible for architecture/security review, but are not part of the first reusable pattern release.

### PAT-005 - Data Ingestion Landing Zone

Ingestion and storage foundation centred on object storage, structured datasets, identity controls, and landing-zone access patterns.

- Status: `candidate_requires_review`
- Release bucket: `candidate_requires_review`
- First-release treatment: Candidate or appendix item until architecture confirms repeatability beyond the current representative project.
- Runtime type: `Data foundation`
- Project count: `1`
- Required building blocks: `bigquery, bucket, environment, iam, keys, network`
- Optional building blocks: `none`
- Representative examples: `vf-gned-nwpdfd-nonlive`

Underlying Terraform module mapping:

- `bigquery` -> `bigquery`, `bigquery_table`
- `bucket` -> `gcs`
- `environment` -> *(template-level config — no GCP modules)*
- `iam` -> `iam_service_account`, `project_iam`, `iam_custom_role_stack`, `service_agent_iam`
- `keys` -> `kms`
- `network` -> `network`, `firewall`, `dns`, `external_global_address`, `external_global_loadbalancer`

### PAT-006 - Specialized VM Workload Platform

VM-centric stack with network, firewall, and relational database resources for proprietary or specialised software that cannot run in containers.

- Status: `reference_specialized`
- Release bucket: `reference_specialized`
- First-release treatment: Reference-only specialized workload until more reusable VM workload demand is confirmed.
- Runtime type: `Specialized VM`
- Project count: `2`
- Required building blocks: `bastion, iam, keys, network, security_policy, sql, vm_workload`
- Optional building blocks: `none`
- Representative examples: `vf-gned-nwparcgis-live, vf-gned-nwparcgis-nonlive`

Underlying Terraform module mapping:

- `bastion` -> `bastion_vm`
- `iam` -> `iam_service_account`, `project_iam`, `iam_custom_role_stack`, `service_agent_iam`
- `keys` -> `kms`
- `network` -> `network`, `firewall`, `dns`, `external_global_address`, `external_global_loadbalancer`
- `security_policy` -> `vf_security_policy`
- `sql` -> `cloud_sql`
- `vm_workload` -> `compute_instance`, `compute_disk`, `compute_resource_policy`
