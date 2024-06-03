# Privileged Containers and Application Authorization with Service Accounts

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/authsa.jpg?raw=true" alt="authsa" width="300" height="300">
</div>

## Objective

Learn how to manage privileged containers and use service accounts for application authorization in OpenShift.

## Prerequisites

- Access to an OpenShift cluster or a terminal emulator connected to one.
- Basic understanding of Kubernetes security mechanisms, including SCCs and RBAC.
- Familiarity with YAML syntax for configuring service accounts and roles.

## Introduction

In the fortified kingdom of OpenShift, some tasks require elevated privileges, much like certain castle tasks needing access to restricted areas. While these tasks pose security risks, proper management through Security Context Constraints (SCCs) and Role-Based Access Control (RBAC) ensures that only trusted entities gain such access. This section delves into handling privileged containers and authorizing applications using service accounts.

## Privileged Containers

Privileged containers are akin to granting a select few individuals access to the castle's secret tunnels and armory. These containers require access to the host's runtime environment, which introduces security risks. To mitigate these risks, SCCs are used to enable and manage privileged access.

### Enabling Privileged Access

To allow containers to run with privileged access, you need to create service accounts specifically configured for this purpose.

1. **Create a Service Account**: First, create a service account for the application needing privileged access. Specify the namespace if required:

    ```bash
    oc create serviceaccount privileged-account -n namespace
    ```

2. **Grant Privileged SCC**: Associate the service account with the `privileged` SCC:

    ```bash
    oc adm policy add-scc-to-user privileged -z privileged-account -n namespace
    ```

3. **Assign the Service Account to a Pod**: Modify the pod or deployment to use the newly created service account:

    ```bash
    oc set serviceaccount deployment/<deployment-name> privileged-account -n namespace
    ```

By following these steps, you ensure that only designated containers gain the necessary privileges, much like a trusted knight given keys to the castle's armory.

## Application Authorization with Service Accounts

In the kingdom of OpenShift, applications need explicit permission to access certain areas, much like artisans needing permits to work in specialized workshops. This is managed through RBAC and service accounts.

### Role-Based Access Control (RBAC)

RBAC in OpenShift is preconfigured to control access to the Kubernetes API. Applications require explicit RBAC authorization to access restricted APIs, ensuring that only authorized entities interact with sensitive resources.

### Using Service Accounts for Authorization

A service account in Kubernetes represents the identity of an application running in a pod. Here's how to grant an application access to the Kubernetes API using service accounts:

1. **Create a Service Account**: Create a service account within the project:

    ```bash
    oc create serviceaccount app-service-account -n namespace
    ```

2. **Grant API Access**: Assign the necessary roles to the service account to grant access to the Kubernetes API:

    ```bash
    oc adm policy add-role-to-user <role> -z app-service-account -n namespace
    ```

3. **Assign the Service Account to Pods**: Update the application's pods or deployments to use the service account:

    ```bash
    oc set serviceaccount deployment/<deployment-name> app-service-account -n namespace
    ```

### Default Service Account

If a service account is not explicitly assigned to a pod, the pod uses the `default` service account, which typically has no special permissions in OpenShift. This ensures a baseline level of security, preventing unintended access to sensitive resources.

## Conclusion

Managing privileged containers and application authorization in OpenShift is crucial for maintaining security and control within the cluster, much like safeguarding the inner workings of a castle. By properly using SCCs and service accounts, administrators can ensure that only trusted applications and containers gain the access they need while minimizing security risks. This approach helps maintain a secure and well-functioning environment, protecting both the infrastructure and its inhabitants from potential threats.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>