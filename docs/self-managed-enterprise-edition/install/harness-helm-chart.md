---
title: Helm installation requirements and included components
sidebar_label: Requirements and included components
description: Requirements for using Helm installation for the on-prem Harness Self-Managed Enterprise Edition.
sidebar_position: 1
helpdocs_topic_id: nsx1d4z86l
helpdocs_category_id: 66qbyn7ugu
helpdocs_is_private: false
helpdocs_is_published: true
redirect_from:
  - /docs/self-managed-enterprise-edition/self-managed-helm-based-install/harness-helm-chart/
canonical_url: https://www.harness.io/blog/getting-started-with-helm
---

Harness recommends Helm package manager for the installation and deployment of Self-Managed Enterprise Edition. Helm offers benefits including:

* Declarative and dynamic application management
* Built-in scalability
* Chart reuse across environments
* Repeatable results you can automate

The Harness Helm chart packages the core modules and components that are required to operate Harness at scale.

For instructions on installing Self-Managed Enterprise Edition using Helm, go to [Install using Helm](/docs/self-managed-enterprise-edition/install/install-using-helm).

## Requirements

The following infrastructure is required to install Self-Managed Enterprise Edition using Helm.

:::info note

Support each node with 8 cores vCPU and a minimum of 32 GB memory.

:::

### Production environment deployment infrastructure

import Infra from '/docs/self-managed-enterprise-edition/shared/prod-env-infra.md';

<Infra />

### Development environment deployment infrastructure

import Infra2 from '/docs/self-managed-enterprise-edition/shared/dev-env-infra.md';

<Infra2 />

## Included components

Harness Helm chart includes the following components.

**Table 1. Platform components for Continuous Delivery**

| **Component** | **Description** |
| :-- | :-- |
| **Access control** | Provides pipelines with access controls including Kubernetes Role-Based Access Control (RBAC). |
| **Data capture** | Responsible for the capture of data related to the operation of Harness Pipelines, including but not limited to events, tasks, metrics, and logs. |
| **CV Nextgen** | Provides continuous verification (CV) services to Pipeline components including deployments, services, and logs. Aggregates data from multiple providers, including performance metrics, from monitoring activities for dashboard presentation. |
| **Gateway** | Manages application gateway services across Harness Pipelines. |
| **Harness Manager** | Responsible for the analysis and presentation of actionable data from the end-to-end Harness Pipeline in an administrative user interface. |
| **Harness Storage Proxy** | Supplies proxy services for storage. |
| **LE Nextgen** | Supplies Harness Learning Engine (LE), a machine-learning component used to fine-tune Pipelines and identify and flag anomalies. |
| **Log service** | Provides frontend logging services to Harness Pipelines. |
| **MinIO** | A distributed object storage system providing Kubernetes-based, S3-compatible storage. You can use MinIO to store runtime logs (build logs) for Harness Pipelines. |
| **MongoDB** | A NoSQL database offering high-volume storage of data represented as key-value pairs contained in documents and collections of documents. |
| **NextGen UI** | Provides the user interface for Harness NextGen. |
| **NgAuth UI** | User interface component for the AngularJS `ng-auth` authentication service. |
| **NgManager** | Provides NextGen Harness Manager. |
| **Pipeline service** | Supports creating a pipeline. |
| **Platform service** | Represents the Harness Platform service. |
| **Redis** | Provides services for Redis, an in-memory data structure store. |
| **Scm service** | Provides source code management services. |
| **Template service** | Provides Harness templates to enable the design of reusable content, logic, and parameters in Pipelines. |
| **Test Intelligence Service** | Provides the Test Intelligence service. |
| **TimescaleDB** | Provides the TimescaleDB time-series SQL database. |


**Table 2. Harness Platform components**

The following components are included in addition to the Harness Platform components.

| **Component** | **Module** |
| :-- | :-- |
| **Ci-manager** | Continuous Integration |
| **Sto-core** | Enables the creation and management of Harness Security Testing Orchestration |
| **Sto-manager** | Provides core services for Harness Security Testing Orchestration |

**Table 3. Optional dependencies**

| **Dependency** | **Description** |
| :-- | :-- |
| **Istio** | [Istio](https://istio.io/latest/about/service-mesh/) is an open-source service mesh. |
| **Ingress Controller** | Supported by default. |
