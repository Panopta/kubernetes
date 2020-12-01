# Panopta Kubernetes Integration

## Prerequisites
* A Kubernetes cluster configured with kubectl

## Deploying Panopta
**Note:** If your cluster already has `metrics-server` installed, disable it as described below.
1. Add this Helm repo using `helm repo add panopta https://panopta.github.io/kubernetes/repo`
2. Install Panopta using `helm install --set customer_key=YOUR-CUSTOMER-KEY <name-of-release> panopta/panopta`

In a few minutes, your cluster should show up in the Panopta control panel.

### A Note on `metrics-server`
The chart will install [metrics-server](https://github.com/kubernetes-sigs/metrics-server) by default. If you already have metrics-server installed in your cluster, you can skip it with `--set metricsServer.install=false`

### Advanced configuration
If you wish to further customize your Panopta deployment, you can pass additional options to the install command by adding one to many  
`--set <key>=<value>`  
to the install command.  
Below is a table of available configuration options.  
You can also specify such options in a YAML-formatted `values.yaml` file which you can then pass along to the install command with `-f values.yaml`

### Configuration Options

| Key Name                  | Default                                    | Description                                                                                                              |
|---------------------------|--------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| customer_key              | None (Required)                            | Your Panopta customer key                                                                                                |
| clusterName               | Kubernetes Cluster                         | The name of this cluster as it will show up in the controlpanel                                                          |
| metricsServer.install     | true                                       | Whether to install metrics-server as part of the deployment. Set to `false` if it's already installed.                   |
| topNNamespaces            | 0                                          | Number of namespaces to pull in, ordered by number of pods. 0 to include all.                                            |
| onsightRequests.cpu       | 3.0                                        | Requested CPU for the Panopta OnSight                                                                                    |
| onsightRequests.memory    | 3Gi                                        | Requested Memory for the Panopta OnSight                                                                                 |
| agent_config              | None                                       | Any additional blocks of configuration to deploy onto the nodes' agents                                                  |

## Upgrading Panopta
1. Fetch the new chart using `helm repo update`
2. Upgrade your deployment using `helm upgrade <deployment name> panopta/panopta`

## Uninstalling Panopta
Run `helm uninstall <release_name>`

You can find the name of the release with `helm ls`
