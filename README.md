# Kubernetes Dashboard Helm Chart

This Helm chart deploys the [Kubernetes Dashboard](https://kubernetes.github.io/dashboard/) along with a Service Account and ClusterRoleBinding for administrative access.

## Table of Contents

- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Uninstallation](#uninstallation)
- [License](#license)

## Introduction

The Kubernetes Dashboard is a web-based UI for managing Kubernetes clusters. This Helm chart deploys the dashboard along with a sample user setup for administrative access.

## Prerequisites

- Kubernetes 1.21+
- Helm 3.0+
- Cluster-admin privileges to deploy the dashboard and create necessary Service Accounts and ClusterRoleBindings.

## Installation

To install the chart with the release name `kubernetes-dashboard`:

```bash
helm repo add kubernetes-dashboard https://kubernetes.github.io/dashboard/
helm install kubernetes-dashboard ./kubernetes-dashboard
```

## Configuration
The following table lists the configurable parameters of the chart and their default values:
|Parameter|Description|Default|
|adminUser.name|Name of the Service Account|admin-user|
|namespace|Namespace where the dashboard is deployed|kubernetes-dashboard|
|kubernetes-dashboard.enabled|Whether to enable the Kubernetes Dashboard|true|

You can specify each parameter using the `--set key=value[,key=value]` argument to helm install.
Example:
helm install kubernetes-dashboard ./kubernetes-dashboard --set adminUser.name=my-admin

## Usage
Accessing the Dashboard

1. Use the following command to get the Bearer Token for the admin-user Service Account:
`kubectl -n kubernetes-dashboard create token admin-user`
Alternatively, you can get the long-lived token stored in the secret:
`kubectl get secret admin-user -n kubernetes-dashboard -o jsonpath="{.data.token}" | base64 --decode`
2. Open a web browser and navigate to the Kubernetes Dashboard URL.

3. Use the retrieved token to log in to the dashboard.

## Upgrading the Chart
To upgrade the chart to a new version, use the following command:
`helm upgrade kubernetes-dashboard ./kubernetes-dashboard`

## Uninstallation
To uninstall the kubernetes-dashboard chart:
`helm uninstall kubernetes-dashboard`
This command removes all the Kubernetes components associated with the chart and deletes the release.

## License

This project is licensed under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0).