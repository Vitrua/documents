# Limiting Workloads

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/limwork.jpg?raw=true" alt="limwork" width="300" height="300">
</div>

## Objective

Learn how to manage and limit workloads in Kubernetes and OpenShift by using resource limits, requests, and quotas to ensure cluster efficiency and prevent resource contention.

## Introduction

In the kingdom of OpenShift, managing resources efficiently is crucial for maintaining harmony and preventing conflicts among the various guilds (workloads). Administrators, akin to wise stewards, use tools such as Role-Based Access Control (RBAC) to grant permissions for workload creation. However, to ensure the kingdom's resources are used wisely and fairly, additional measures such as resource limits, requests, and quotas are implemented. These measures act as the kingdom's laws, ensuring that no single guild consumes excessive resources or impacts others negatively.

## Resource Quotas

Resource quotas are established within namespaces to ensure that workloads do not exceed predefined resource usage limits. This is similar to allocating specific amounts of resources to different guilds within the castle, ensuring that each guild has enough to operate but not so much that they deplete the kingdom's resources.

### Example Resource Quota

Here is an example of creating a resource quota in a namespace:

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: memory
  namespace: example
spec:
  hard:
    limits.memory: 4Gi
    requests.memory: 2Gi
  scopes: {}
  scopeSelector: {}
```

### Explanation

- **apiVersion**: Specifies the API version for the resource.
- **kind**: Defines the type of resource, in this case, ResourceQuota.
- **metadata**: Contains metadata for the resource, such as the name (`memory`) and the namespace (`example`).
- **spec**: Defines the specifications for the resource quota.
  - **hard**: Lists the hard limits for resource usage.
    - **limits.memory**: Maximum amount of memory that workloads in the namespace can use.
    - **requests.memory**: Maximum amount of memory that workloads in the namespace can request.
  - **scopes** and **scopeSelector**: Define which namespace resources the quota applies to.

The *hard* key lists the restrictions, much like decrees from the king limiting how much of a certain resource each guild can consume.

### Compute Quotas

Compute quotas that you can include in the *hard* key are:
- **limits.cpu**
- **limits.memory**
- **requests.cpu**
- **requests.memory**

Limit quotas control the maximum compute resources that workloads in a namespace can consume, while request quotas control the maximum resources that workloads in a namespace can reserve. Excessive quotas can cause resource underutilization and unnecessarily limit workload performance. Therefore, it's crucial to balance these quotas carefully.

### Object Count Quotas

In addition to compute quotas, a quota can also limit the number of resources of a given type in a namespace. Setting object count quotas can limit the damage from accidents and maintain adequate cluster performance. This is akin to limiting the number of guild members to prevent overcrowding in the castle.

### Example Object Count Quota

To set a quota for resources of the core group, use the `count/resource_type` syntax. Use the `oc api-resources` command with an empty api-group parameter to list resources of the core group:

```bash
oc api-resources --api-group="" --namespaced=true
```

This command helps you determine the resource types available for setting quotas, ensuring that you have a comprehensive understanding of the resources within your cluster.

## Conclusion

In the realm of OpenShift, managing and limiting workloads through resource quotas, limits, and requests ensures that the kingdom's resources are used efficiently and fairly. By setting these boundaries, administrators can prevent resource contention and ensure smoother cluster operation, much like a wise steward managing the resources of a vast and bustling castle.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>