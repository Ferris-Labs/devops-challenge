# ferris labs - DevOps-challenge

### How would you solve the following DevOps challenge?

## Context & Background

The ferrisDX platform consists of the following technical FOSS components engineered to work as an
**event-based micro-services integration platform** on top of any Kubernetes or dedicated compute
infrastructure. It is designed to be **cloud native** and abstracted away from hyperscaler propietary
services. It uses the following components under the hood:

* ArgoCD
* Consul
* Kafka
* Minio
* PostGreSQL
* Vault
* Keycloak
* Elastic
* Flask

As optional components depending on the use case of the clients the following application level containers
can be added to the platform - either by being deployed alongside in the ferris K8S namespace or by utilzing
and connecting to existing client implementations:

* Theia based IDEs
* JupyterHub Notebook Server
* Presto or Trino SQL abstraction layers
* any DB flavor (RDBMS, DocDBs, GraphDBs, other)

It utilises the following set of open standards throughout the components and every addition or change
needs to adhere to these standards or impose an additional (equally open and universal) standard that
does not confilct with the existing ones.

* OpenAPI - REST and Async (for all services)
* Cloud Events (for all event wrappings)
* S3 (for any file abstraction)
* JDBC / SQLAlchemy for any DB abstraction

## DevOps Challenge Objective

We have a dedicated set of Helm charts and Moustache scripts to deploy a new instance of ferrisDX based on a client
and base infrastructure specific config file. This instance specific configuration is generated via a wizard based
process and results in a structured JSON message on an internal ferris event kafka topic. A set of dedicated Helm
charts then uses this config / setup message and deploys the new ferrisDX instance to a cloud provider of choice
(currently GCP, Azure, Redhat and T-Systems)

### Design Goal

Think of an approach that allows us to monitor and account for infrastructure usage. Automate the *Usage Tracking*
for the following scenarios in a generic and re-usable fashion:

1. a single user minimum setup of ferrisDX only consisting of the bare minimum components (ArgoCD, Consul, Minio,
Kafka, PostGreSQL, KeyCloak, Vault and the ferris UI as Flask admin web-app) on GCP
1. a team setup including the same setup as above but also linking to an Azure Databricks cluster that is connected
to ferrisDX but which is not relevant to the accounting / tracking.
1. a hybrid setup spanning an on-prem instance (on the company's K8S) and a GCP instance with additional containers
running IDEs, a JupyterHub Server and a Presto cluster in addition to the base setup

Remember that you can utilize all of the components in play on the ferrisDX platform already and that you do
NOT have to reinvent the wheel.

## Requirements

The additional approach to monitoring & accounting / tracking to be designed needs to:
* work out of the box for any new (auto-deployed) ferrisDX platform
* become an integrated part of ferrisDX (either in the background as service, event flow or as its own component)
* have its independent lifecycle with minimum (hard) dependencies on other components
* establish an *Usage Tracking Standard* to be used across any scenarion similar to the ones stated above

The new approach to "Usage Tracking" can:
* use an existing standard (if it fits the picture and is extensible)
* extend an existing standard
* define a new skeleton for the currently known aspects

## Challenge Response

At a minimum write your response as **response.md** to this repository. You additionally can:
* cross-reference any links to documentation / standards / components you would use / apply
* include schematics for how you would envision such a "usage tracking" to work
* include a rough breakdown of which elements you would deliver when along 2 week sprints
* use our second interview as an opportunity to discuss and clarify any questions

Please commit and push your response at your convenience within the next 7 business days and
drop us a quick mail at [tom@ferrislabs.net](mailto://tom@ferrislabs.net) as soon as you have pushed.

