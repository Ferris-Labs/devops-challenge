# ferris labs - DevOps-challenge

## Design Goal

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

## Solution

Please check the usage_tracking_diagram.png as it explains my idea. 

As the ELK stack is in use I think that we could use it also for the metrics. It should also report the resource limits of the workloads. If not, we could take this from Kafka or any other place. This is needed for the calculation of the used / unused capacity.

All project entities will be created inside the K8S as separate namespaces. I assume that this is the current configuration, if not we should do this. This is going to give us isolation and a way to calculate consumed resources.

### Data flow

1. Elastic agent will collect for us the needed statistics and will send them to the ELK cluster.

1. usage-trckng service - The purpose of this new service is to pull information from multiple places (ELK, GCP API) in order to do the needed calculations. From ELK it will calculate the resources that were consumed filtered by the name of the namespace. By doing this, we will know the usage ratio of every entity. Based on this usage ratio, we can calculate the price as we will take the total amount from GCP API. In the end, this information can be written in PSQL DB.

The service might be a Kubernetes CronJob if we do not need this information in real-time.

1. The data that has just been written in the PSQL can be consumed by the ferris-ui service and shown to the users.

### Links

* https://www.elastic.co/downloads/elastic-agent
* https://www.elastic.co/guide/en/observability/current/kubernetes-pod-metrics.html
