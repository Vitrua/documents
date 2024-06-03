# Scoping Application Access to Kubernetes API Resources

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/kapires.jpg?raw=true" alt="kapires" width="300" height="300">
</div>

## Objective

Understand how to manage and scope application access to Kubernetes API resources within OpenShift, ensuring applications have the necessary permissions while adhering to the principle of least privilege.

## Prerequisites

- Access to an OpenShift cluster or a terminal emulator connected to one.
- Understanding of Kubernetes RBAC (Role-Based Access Control) and service accounts.
- Basic knowledge of YAML syntax for creating and editing configuration files.

## Introduction

In the OpenShift kingdom, applications often need access to various resources, much like how different roles within a castle require access to specific rooms and areas. Properly scoping this access ensures security and functionality without over-provisioning permissions.

## Accessing API Resources in the Same Namespace

To grant an application access to resources within the same namespace, you need to follow a process similar to granting a castle guard access to a specific wing of the castle.

### Steps:

1. **Create a Role or Cluster Role**: Define the permissions required for the application within the namespace.
2. **Create a Service Account**: This service account represents the application's identity within the namespace.
3. **Create a Role Binding**: Associate the service account with the role, allowing it to perform the actions specified by the role on the resource.

### Example:

Creating a role and binding it to a service account within the same namespace:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: example-namespace
  name: pod-reader
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: example-sa
  namespace: example-namespace
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods
  namespace: example-namespace
subjects:
- kind: ServiceAccount
  name: example-sa
  namespace: example-namespace
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

## Accessing API Resources in a Different Namespace

When an application needs access to resources in a different namespace, it's like granting a guard access to a different wing of the castle. You need to create the role binding in the namespace where the resource resides and reference the service account from the other namespace.

### Steps:

1. **Create a Role in the Target Namespace**: Define the permissions required for the application within the target namespace.
2. **Create a Role Binding in the Target Namespace**: Bind the role to the service account from the other namespace using the `system:serviceaccount` format.

### Example:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: target-namespace
  name: secret-reader
rules:
- apiGroups: [""]
  resources: ["secrets"]
  verbs: ["get", "watch", "list"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-secrets
  namespace: target-namespace
subjects:
- kind: ServiceAccount
  name: example-sa
  namespace: source-namespace
  apiGroup: ""
roleRef:
  kind: Role
  name: secret-reader
  apiGroup: rbac.authorization.k8s.io
```

In the `subjects` field, `system:serviceaccount:source-namespace:example-sa` is used to reference the service account from the other namespace.

## Accessing API Resources in All Namespaces

To grant an application access to resources across all namespaces, you must use a cluster role binding, similar to giving a high-ranking official keys to all the castle's wings.

### Steps:

1. **Create a Cluster Role**: Define the global permissions required by the application.
2. **Create a Cluster Role Binding**: Associate the cluster role with the application service account, granting it access across the entire cluster.

### Example:

Creating a cluster role and binding it to a service account for access across all namespaces:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: cluster-secret-reader
rules:
- apiGroups: [""]
  resources: ["secrets"]
  verbs: ["get", "watch", "list"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: read-secrets-global
subjects:
- kind: ServiceAccount
  name: example-sa
  namespace: example-namespace
roleRef:
  kind: ClusterRole
  name: cluster-secret-reader
  apiGroup: rbac.authorization.k8s.io
```

In this setup, the service account `example-sa` in the namespace `example-namespace` is granted cluster-wide access to read secrets.

## Conclusion

By carefully scoping application access to Kubernetes API resources, you ensure that applications have the permissions they need while maintaining the security and integrity of the cluster. This approach mirrors how a castle manages access to its various areas, granting specific keys to different roles to maintain order and security.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>