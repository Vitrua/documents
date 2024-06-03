# Use Cases for Kubernetes API Access

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/kapiaccess.jpg?raw=true" alt="kapiaccess" width="300" height="300">
</div>

## Objective

Understand how to manage Kubernetes API access for different types of infrastructure applications in OpenShift, including monitoring applications, controllers, and operators.

## Prerequisites

- Access to an OpenShift cluster or a terminal emulator connected to one.
- Understanding of Kubernetes API and role-based access control.
- Basic knowledge of YAML syntax for defining roles and bindings in Kubernetes.

## Introduction

In the OpenShift kingdom, various entities require special permissions to monitor or modify the cluster, much like how different roles in a castle—guards, overseers, and engineers—need specific access rights to perform their duties. These entities are categorized into monitoring applications, controllers, and operators, each needing tailored access to the Kubernetes API.

## Application Kubernetes API Authorization with Roles

To provide applications with the necessary permissions while adhering to the principle of least privilege, you can create roles or cluster roles. These roles describe the specific permissions required by the application, similar to how a castle might grant different keys to its staff to access only the areas they need for their duties.

### Example: Creating a Cluster Role

A cluster role might be necessary for an application that needs to read secrets across all namespaces. This is akin to giving the castle's master key to a trusted advisor who needs to access various rooms for inspection:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: secret-reader
rules:
- apiGroups: [""]
  resources: ["secrets"]
  verbs: ["get", "watch", "list"]
```

In this configuration:
- `apiGroups: [""]` refers to the core API group.
- The role grants permissions to `get`, `watch`, and `list` secrets.

OpenShift includes predefined cluster roles such as `edit`, which allows applications to create and update most objects, much like how the castle steward can modify room arrangements as needed.

## Binding Roles to Service Accounts

To grant an application the permissions defined in a role, you must bind the role to the application's service account. This is similar to officially assigning keys to different castle staff.

### Binding a Role to a Service Account

Use the following command to bind a role to a service account, akin to handing over the key to a specific room:

```bash
oc adm policy add-role-to-user secret-reader -z app-service-account
```

### Creating a Cluster Role Binding

For cluster-wide permissions, use this command to grant broader access, like giving the head guard keys to multiple sections of the castle:

```bash
oc adm policy add-cluster-role-to-user secret-reader app-service-account
```

## Assigning an Application Service Account to Pods

OpenShift uses RBAC to manage resource access based on the roles associated with the service account. To ensure that an application uses the assigned permissions, you need to specify the service account in the pod definition. This ensures that the right person is accessing the right part of the castle.

### Specifying the Service Account in the Pod Definition

In the pod definition, set the `spec.serviceAccountName` field to the name of the service account, like assigning a staff member to a specific duty:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: example-pod
spec:
  serviceAccountName: app-service-account
  containers:
  - name: example-container
    image: example-image
```

### Using the Service Account Token

Applications must use the service account token to access the Kubernetes API. Generate and mount the token as a pod volume using the `TokenRequest` API, akin to ensuring the guard has the right key for their assigned post.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: example-pod
spec:
  serviceAccountName: app-service-account
  containers:
  - name: example-container
    image: example-image
    volumeMounts:
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: token
  volumes:
  - name: token
    projected:
      sources:
      - serviceAccountToken:
          path: token
          expirationSeconds: 7200
```

In this example:
- The service account token is mounted as a volume, providing the application with the necessary credentials to access the Kubernetes API.

## Conclusion

Managing Kubernetes API access for infrastructure applications in OpenShift is crucial for maintaining security and ensuring that applications have the permissions they need to function correctly. By defining and binding roles to service accounts and properly configuring pods, you can control access effectively, much like how a castle's hierarchy manages access to its various sections. This ensures a secure, well-functioning environment where each application can perform its duties without compromising the security of the cluster.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>
