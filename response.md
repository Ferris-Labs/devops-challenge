# Overview of Kubernetes monitoring?

Kubernetes makes it easier to run distributed, containerized workloads. But, this model also introduces the complexity of handling distributed and connected compute elements.

In such complex setups, monitoring is crucial to the management of an application’s lifecycle since it helps debug issues that arise when the cluster is operational. Monitoring is the practice of scanning all critical components to ensure there are no single points of failure in a cluster.

Kubernetes monitoring helps to identify performance issues, such as insufficient resources, high CPU usage, pod failures, etc, across their K8s environment. 
It also makes managing your containerized application easier by tracking uptime, utilization of cluster resources, and cluster component interactions.

Some of key objectives of Kubernetes monitoring include:

  * Ensuring resources are consumed optimally by a team or a particular application
  * Balancing loads across instances of the application hosted on separate nodes
  * Automatically taking advantage of newly available resources when a new node joins a cluster
  * Redeploying workloads to other nodes when one host goes down
  * Efficient provisioning of updates and rollbacks when necessary

Kubernetes monitoring is the process of analyzing and managing the performance of containers in the Kubernetes clusters. Although Kubernetes has in-built monitoring plug-ins, they do not provide the granular visibility required for efficient container monitoring and troubleshooting. As Kubernetes needs more than monitoring the CPU, memory, and storage, traditional monitoring tools also can not efficiently monitor the multitude of components enabled by Kubernetes. As a result, several out-of-the-grid monitoring solutions provide timely and efficient visibility of the Kubernetes clusters.


# Kubernetes monitoring metrics

Various metrics help developers ensure production workloads are running efficiently. These metrics are critical events of containers, PODs, nodes as well as the application, that collectively enable monitoring tools to derive a profile from the cluster’s characteristics.

Accurate coordination of metrics is a crucial Kubernetes monitoring best practice. By usage of right-measured metrics can be achieved end-to-end visibility of Kubernetes clusters.

Metrics are essential in setting up dashboard activities and alerts, and they provide insight into both the Kubernetes system and the applications running within it.

Metrics can be fetched from the cAdvisor, Metrics Server, Kubernetes API Server, and Kube-state-metrics, among others.
 
Some of the key metrics you should measure in Kubernetes are: 

**I. Cluster monitoring**

The Kubernetes cluster is the chief host for all containers and the machines that run the applications. Therefore, monitoring its environment and the well-being of its components, such as nodes and pods, is vital to successful container management.
Key elements you should monitor in a Kubernetes cluster are:

**I.1. Cluster nodes**

In a cluster are nodes that enable the running of applications. These nodes comprise several resources that allow them to carry out their function. You must observe these resources and monitor their health. Worker nodes host the containers while the master nodes manage the worker nodes’ activities. 

**I.2. Cluster pods**

A pod is a group of one or more containers. The pods are the smallest units in a cluster. The amount of pods running at a time determines the number of nodes to be deployed. Checking the pod’s health and resource usage is critical to efficient Kubernetes monitoring.

**I.3. Resource utilization**

Understanding this metric reveals the cluster nodes’ strengths and weaknesses and helps to determine what’s sufficient and what’s in excess. You should check for resources, including disk utilization, memory utilization, CPU utilization, network bandwidth, and many others.

**II. Pod monitoring**

A pod is a group of containers deployed into a node. It is foundational to the Kubernetes ecosystem and requires proper monitoring. Following metrics are for efficient pod monitoring:

**II.1. Container metrics**

Excess or insufficient pods could affect the application performance. You must understand the number of containers running in a pod and how to regulate them. Track the cycle of the various containers in your pods, and ensure you only burden each pod with what it can bear. Do not overestimate pod scalability.

**II.2. Application metrics**

Application metrics measure the cycle and performance of the application, providing industry-specific information regarding the business the application was developed for.
In addition, application metrics provide visibility into traffic, the rate of failed requests, the amount of time a request took, the most and the least used features of the applications, and several other vital information.

**II.3. Kubernetes scaling and availability metrics**

The seamlessness of scaling up and down your containers is one of Kubernetes’ key features. Since the number of containers or pods in a cluster determines the number of nodes, understanding the scaling and availability capacities helps in configuring auto-scaling tools for your Kubernetes clusters.

**II.4. Load average**

Load average is a count of programs running or waiting to run in the CPU. As a rule of thumb, you must ensure that your load average does not exceed the number of cores on your host.
While a high load average alone is not always an indicator of a problem, it can become one if it is accompanied by high sys CPU usage or high I/O wait. Therefore, you need to constantly monitor your application’s load average to quickly and efficiently troubleshoot issues if they occur.

I**I.5. Resource request and limit**

Each container has an associated request which runs on a predetermined CPU and memory. The Kubernetes scheduler uses these requests to ensure that only the node with the requisite capacity to host a requesting pod hosts it. 

Both underutilization and overutilization can be disastrous. Underutilization is a situation where the container requests outmatch the actual usage and leads to inefficient resource utilization, which means you are paying for what you are not using.

When the pod’s requests are lower than its actual usage, over-utilization happens, and your applications work slower due to insufficient resources on the node. To avoid these extremes, keep a grip on your nodes’ resource requests and limits. Aim for up to 80% actual usage on the 90th percentile for both resource requests and limits.


# Key methods for monitoring Kubernetes

You can monitor your Kubernetes cluster nodes in two ways: using the daemonsets and heapster. Either help collect metrics from the cluster and transmit these to an external endpoint for further analysis. 

a. Monitoring using Kubernetes DaemonSets

A DaemonSet is a specialized POD that ensures that a snapshot of its workload runs on all nodes within the cluster. Developers can create a DaemonSet that runs a monitoring agent on every node in the cluster to collect performance metrics.

Because it’s easy to provision, plenty of Kubernetes monitoring solutions use a DaemonSet approach to deploy monitoring software on cluster nodes for examining health of the POD along with performance data. The Kubernetes DaemonSets monitors individual pods and ensures each runs on every node in the cluster. It reports the ability of a node to run the pods allotted to it. As a workload tool, object, or specialized pod, it is a monitoring agent that collects critical resource metrics from the containers and the node host and sends them to the API server.

Since the daemonset is a pod itself, you can create your specialized monitoring daemonset, which functions as a sister pod to your nodes. You can thereafter configure Kubernetes to affix this Daemonset to each node you create automatically.
This enables the Daemonset to watch the node and its constituents, and as each node gets terminated either manually (by an admin) or automatically (by Kubernetes self-healers), its designated monitoring daemonset is also terminated.

b. Kubernetes monitoring using [Metrics Server](https://loft.sh/blog/how-to-set-up-metrics-server-an-easy-tutorial-for-k8s-users/)

Formerly known as Heapster before it was deprecated, Metrics Server sends performance data to a storage server designed to obtain cluster statistics. As opposed to a DaemonSet, a Metrics Server acts as a normal POD that collects performance data from the Kubelet service and uses the Metrics API to expose them to the kube-apiserver.

The metrics server is a Kubernetes tool used to gather data on resource usage for pods and nodes in your Kubernetes cluster. It’s built on top of the metrics API, thus you can use it to get metrics such as CPU and memory usage.

You can then use these metrics to determine how to scale your cluster and allocate resources. Since the metric server is deployed as a pod, you can use it to get metrics from different sources like kubelet, Kubernetes API, and cAdvisor.
It serves as a link between the cluster and backend storage that also serves as a log collector. Metrics Server enables performance analysis and visualization.It is highly scalable and is considered capable to monitor clusters of up to 5,000 nodes using a single deployment—an efficient choice for clusters with large workloads.

# Popular K8s monitoring tools

Kubernetes monitoring is the process of analyzing and managing the performance of containers in the Kubernetes clusters. Although Kubernetes has in-built monitoring plug-ins, they do not provide the granular visibility required for efficient container monitoring and troubleshooting. As Kubernetes needs more than monitoring the CPU, memory, and storage, traditional monitoring tools also can not efficiently monitor the multitude of components enabled by Kubernetes. As a result, several out-of-the-grid monitoring solutions provide timely and efficient visibility of the Kubernetes clusters.

Here’s a brief rundown of popular K8s monitoring tools.

**Prometheus**
[Prometheus](https://medium.com/cloud-native-daily/monitoring-kubernetes-pods-resource-usage-with-prometheus-and-grafana-c17848febadc) is an open-source, community-driven monitoring tool managed by the Cloud Native Computing Foundation. This tool stores data as a time series that can easily be accessed via a custom query language, then rendered in a built-in browser presentation.

Through the Prometheus Operator, provisioning its monitoring tool on a Kubernetes cluster is relatively simple compared to other popular tools.

**Kubernetes Dashboard**
Maintained as part of the Kubernetes stack, this [UI-based tool](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/) comes out-of-the-box with plenty of features that allow developers to manage workloads and check run-time resource utilization.

Through a number of different views this tool provides detailed insights including Persistent Volume Claims, ConfigMaps, workload kinds, CPU and memory usage, etc., across all nodes of a cluster.

**The EFK Stack**
EFK is a [stack of tools](https://github.com/kubernetestr/kubernetes-EFK-stack) comprising [ElasticSearch](https://www.elastic.co/elasticsearch/), [Fluentd](https://docs.fluentd.org/v/0.12/articles/kubernetes-fluentd), and [Kibana](https://www.elastic.co/kibana/) that collectively provides logs and critical insights of an operational Kubernetes cluster. These tools work together to:

  * Collect cluster logs (through Fluentd)
  * Store them centrally (ElasticSearch)
  * Visualize the metrics (Kibana UI)

This stack is particularly useful for:

  * Detecting issues as they arise
  * Presenting issues in a simple GUI



# DevOps-challenge

The subject of task in the DevOps challenge is: *"Think of an approach that allows us to monitor and account for infrastructure usage"*.
By my understanding, if I try to categorize the elements that should be monitored, I would define them as "infrastructure resource utilization and costs"
 
So, further I will just introduce and describe two tools, that can enpower monitoring of any (public-cloud or on-premises) Kubernetes infrastructure, with mechanism for resource usage accounting and cost allocation. The main thing in-common for them is  their open-source nature.


# [Kubernetes Opex Analytics](https://rodrigue-chakode.medium.com/kubernetes-resource-usage-analytics-for-cost-allocation-and-capacity-planning-416800e85d16)

**kube-opex-analytics** (literally Kubernetes Opex Analytics) is a Kubernetes usage accounting and analytics tool to help organizations track the resources being consumed by their Kubernetes clusters over time (hourly, daily, monthly). The purpose of kube-opex-analytics is to help prevent overpaying. Indeed, it provides insightful usage analytics metrics and charts, that engineering and financial teams can use as key indicators to take appropriate cost optimization decisions.
The key features are:

  * **Hourly consumption trends, daily and monthly accounting per namespace**. This feature provides analytics metrics tracking both actual usage and requested capacities over time. Metrics are namespaced-based, collected every 5 minutes, consolidated on a hourly basis for trends, from which daily and monthly accounting is processed.
  * **Accounting of non-allocatable capacities.** At node and cluster levels, kube-opex-analytics tracks and consolidates the share of non-allocatable capacities and highlights them against usable capacities (i.e. capacities used by actual application workloads). In contrary to usable capacities, non-allocatable capacities are dedicated to Kubernetes operations (OS, kubelets, etc).
  * **Cluster usage accounting and capacity planning**. This feature makes it easy to account and visualize capacities consumed on a cluster, globally, instantly and over time.
  * **Usage/requests efficiency.** Based on hourly-consolidated trends, this functionality helps know how efficient resource requests set on Kubernetes workloads are, compared against the actual resource usage over time.
  * **Cost allocation and charge back analytics:** automatic processing and visualization of resource usage accounting per namespace on daily and monthly periods.
  * **Insightful and extensible visualization.** kube-opex-analytics enables built-in analytics dashboards, as well as a native Prometheus exporter that exposes its analytics metrics for third-party visualization tools like Grafana.
  
**Design fundamentals**

    kube-opex-analytics periodically collects CPU and memory usage metrics from Kubernetes's API, processes and consolidates them over various time-aggregation perspectives (hourly, daily, monthly), to produce resource usage reports covering up to a year. The reports focus on namespace level, while a special care is taken to also account and highlight shares of non-allocatable capacities.

  * Namespace-focused: Means that consolidated resource usage metrics consider individual namespaces as fundamental units for resource sharing. A special care is taken to also account and highlight non-allocatable resource

  * Hourly Usage & Trends: Like on public clouds, resource consumption for each namespace is consolidated on a hourly-basic. This actually corresponds to the ratio (%) of resource used per namespace during each hour. It's the foundation for cost allocation and also allows to get over time trends about resources being consuming per namespace and also at the Kubernetes cluster scale.

  * Daily and Monthly Usage Costs: Provides for each period (daily/monthly), namespace, and resource type (CPU/memory), consolidated cost computed given one of the following ways: (i) accumulated hourly usage over the period; (ii) actual costs computed based on resource usage and a given hourly billing rate; (iii) normalized ratio of usage per namespace compared against the global cluster usage.

  * Utilization of Nodes by Pods: Highlights for each node the share of resources used by active pods labelled by their namespace.
  
**Usage Accounting Models**

    kube-opex-analytics support various usage accounting models with the aim to address use cases like cost allocation, usage show back, capacity planning, etc.
    The target accounting model must be selected using the startup configuration variable KOA_COST_MODEL using one of the following values:

  * CUMULATIVE_RATIO: (default value) compute costs as cumulative resource usage for each period of time (daily, monthly).
  
  * RATIO: compute costs as normalized ratios (%) of resource usage during each period of time.
  
  * CHARGE_BACK: compute actual costs using a given cluster hourly rate and the cumulative resource usage during each period of time.

**Deployment**
    
kube-opex-analytics requires read-only access to the following Kubernetes API endpoints.  

  * /api/v1
  * /apis/metrics.k8s.io/v1beta1 (provided by [Kubernetes Metrics Server](https://github.com/kubernetes-sigs/metrics-server), which shall be installed on the cluster if it's not yet the case).
    On a typical deployment inside the Kubernetes cluster, the following Kubernetes API base URL shall be used: https://kubernetes.default.

kube-opex-analytics can be installed using one of the following methods:

  * [Installation using kubectl and Kustomize](https://github.com/rchakode/kube-opex-analytics/blob/main/docs/installation-on-kubernetes.md#installation-using-kubectl-and-kustomize)
  * [Installation using Helm](https://github.com/rchakode/kube-opex-analytics/blob/main/docs/installation-on-kubernetes.md#installation-using-kubectl-and-kustomize)
  
  The Helm deploys an HTTP service named kube-opex-analytics on port 80 in the selected namespace, providing to the built-in dashboard of kube-opex-analytics

 
# [OpenCost](https://www.opencost.io/)


OpenCost is a vendor-neutral open source project for measuring and allocating infrastructure and container costs in real time. Built by Kubernetes experts and supported by Kubernetes practitioners, OpenCost shines a light into the black box of Kubernetes spend.

OpenCost models give teams visibility into current and historical Kubernetes spend and resource allocation. These models provide cost transparency in Kubernetes environments that support multiple applications, teams, departments, etc.

OpenCost was originally developed and open sourced by [Kubecost](https://www.kubecost.com/). [OpenCost project](https://github.com/opencost/opencost) combines a [specification](https://github.com/opencost/opencost/blob/develop/spec/opencost-specv01.md) as well as a Golang implementation.  

Here is a summary of features enabled:

  * Real-time cost allocation by Kubernetes cluster, node, namespace, controller kind, controller, service, or pod
  * Dynamic onDemand asset pricing enabled by integrations with AWS, Azure, and GCP billing APIs
  * Supports on-prem k8s clusters with custom CSV pricing
  * Allocation for in-cluster resources like CPU, GPU, memory, and persistent volumes.
  * Easily [export pricing data to Prometheus](https://www.opencost.io/docs/prometheus) with /metrics endpoint
  * Free and open source distribution (Apache2 license)


**Setup**

You can [deploy OpenCost](https://www.opencost.io/docs/install) on any Kubernetes 1.8+ cluster in a matter of minutes.


**Usage**

  OpenCost can be explored and used by several ways:

  * [Cost APIs](https://www.opencost.io/docs/api)
  * [CLI / kubectl cost](https://www.opencost.io/docs/kubectl-cost)
  * [Prometheus Metrics](https://www.opencost.io/docs/prometheus)
  * Reference [User Interface](https://github.com/opencost/opencost/tree/develop/ui)
  
A valueable presentation for **Cloud Cost Monitoring with OpenCost and Kubernetes Optimization Strategies** can be watched [here](https://www.youtube.com/watch?v=YnEhvuYp6UQ).








