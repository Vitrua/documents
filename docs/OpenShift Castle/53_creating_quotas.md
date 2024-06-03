# Creating Quotas Across Multiple Projects

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/creaquo.jpg?raw=true" alt="creaquo" width="300" height="300">
</div>

## Objective

Learn to create and manage cluster resource quotas in OpenShift to ensure fair resource allocation across multiple projects, using both the web console and command-line interface.

## Prerequisites

- Access to an OpenShift cluster or a terminal emulator connected to one.
- Basic understanding of Kubernetes and OpenShift resource management concepts.
- Familiarity with ClusterResourceQuota and its configuration.
- Knowledge of YAML syntax for creating and editing configuration files.
- Basic command-line skills for using the OpenShift CLI (`oc` commands).

## Introduction

In the kingdom of OpenShift, managing resources fairly across multiple projects (guilds) is crucial for maintaining harmony and efficiency. Cluster resource quotas are the kingdom's overarching laws, ensuring that no single guild consumes more than its fair share of resources, thus preserving balance and order throughout the realm.

## Creating Cluster Resource Quotas

Cluster resource quotas in OpenShift follow a structure similar to namespace resource quotas but include selectors to specify which namespaces the quota applies to. These quotas act like royal decrees that apply across multiple guilds, ensuring equitable resource distribution throughout the kingdom.

### Example of ClusterResourceQuota

Here is an example of a `ClusterResourceQuota` resource:

```yaml
apiVersion: quota.openshift.io/v1
kind: ClusterResourceQuota
metadata:
  name: example
spec:
  quota:
    hard:
      limits.cpu: 4
  selector:
    annotations: {}
    labels:
      matchLabels:
        kubernetes.io/metadata.name: example
```

### Explanation

- **apiVersion**: Specifies the API version.
- **kind**: Defines the resource type, which is `ClusterResourceQuota`.
- **metadata**: Contains metadata about the resource, such as its name.
- **spec**: Contains the specifications for the quota.
  - **quota**: Defines the resource limits.
    - **hard**: Lists the resource limits, such as CPU.
  - **selector**: Specifies which namespaces the quota applies to, using annotations and labels to match namespaces.

### Using the Web Console

To create a cluster resource quota using the web console, navigate to **Administration** > **CustomResourceDefinitions**. This method provides a user-friendly interface, much like the grand chamber where the kingdom's overseers (administrators) draft and implement royal decrees.

### Using the Command-Line Interface

Alternatively, you can use the `oc create clusterresourcequota` command to create a cluster resource quota. For example:

```bash
oc create clusterresourcequota example --project-label-selector=group=dev --hard=requests.cpu=10
```

This command is akin to issuing a royal decree that applies across multiple guilds, ensuring fair resource allocation throughout the kingdom.

### Example Explanation

- **oc create clusterresourcequota example**: Creates a cluster resource quota named `example`.
- **--project-label-selector=group=dev**: Applies the quota to projects with the label `group=dev`.
- **--hard=requests.cpu=10**: Sets a hard limit of 10 CPU requests for the selected projects.

### Reviewing Quota Usage

OpenShift creates resources of the `AppliedClusterResourceQuota` type in namespaces affected by cluster resource quotas. Project administrators can review quota usage by examining these resources, much like how royal inspectors review compliance with the kingdom's laws.

For example, use the following command to describe an `AppliedClusterResourceQuota`:

```bash
oc describe AppliedClusterResourceQuota -n example-2
```

This command provides detailed information about the quota usage in the specified namespace, ensuring transparency and accountability in resource allocation.

## Conclusion

Creating and managing cluster resource quotas in OpenShift ensures fair resource distribution across multiple projects, maintaining harmony and efficiency in the digital kingdom. By using both the web console and command-line interface, administrators can easily implement and monitor these quotas. Reviewing `AppliedClusterResourceQuota` resources helps ensure compliance with the quotas, much like royal inspectors ensuring that guilds adhere to the kingdom's laws. This balanced approach ensures that all projects have the resources they need to thrive, preserving the kingdom's stability and prosperity.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>