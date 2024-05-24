# Managing RBAC with the CLI

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/rbaccli.jpg?raw=true" alt="rbaccli" width="300" height="300">
</div>

## Objective

This guide will show you how to manage Role-Based Access Control (RBAC) in Red Hat OpenShift Container Platform (RHOCP) using the command-line interface (CLI). You'll learn how to assign and remove roles, manage cluster and namespace roles, and use the `oc adm policy` command for various RBAC operations.

## Prerequisites

- Access to an OpenShift cluster with the `oc` CLI installed.
- Basic knowledge of OpenShift and RBAC concepts.

## Introduction

In the medieval kingdom of OpenShift, roles and responsibilities are critical to maintaining order and ensuring the efficient management of resources. The King, represented by the cluster administrator, must delegate tasks and privileges wisely to ensure the realm runs smoothly. This guide will help you navigate the complexities of Role-Based Access Control (RBAC), much like a royal advisor guiding the king in appointing trusted stewards.

## Managing RBAC with the CLI

### Cluster Roles and Local Roles

OpenShift defines two main types of roles:

- **Cluster Roles**: These roles apply across the entire cluster and are managed by cluster administrators.
- **Local Roles**: These roles apply within a specific project (namespace) and are managed at the project level.

### Adding a Cluster Role to a User

To grant a user a cluster-wide role, the King can issue a decree using the following command:

```bash
oc adm policy add-cluster-role-to-user <cluster_role> <username>
```

For example, to make "arthur" a cluster administrator:

```bash
oc adm policy add-cluster-role-to-user cluster-admin arthur
```

### Changing a Regular User to a Cluster Administrator

To elevate a regular user to the status of a cluster administrator, use:

```bash
oc adm policy add-cluster-role-to-user cluster-admin <username>
```

Example:

```bash
oc adm policy add-cluster-role-to-user cluster-admin arthur
```

### Removing a Cluster Role from a User

If a noble knight must be relieved of their duties, the following command can be used:

```bash
oc adm policy remove-cluster-role-from-user <cluster_role> <username>
```

For instance, to revoke the cluster-admin role from "arthur":

```bash
oc adm policy remove-cluster-role-from-user cluster-admin arthur
```

### Changing a Cluster Administrator to a Regular User

To demote a cluster administrator back to a regular user:

```bash
oc adm policy remove-cluster-role-from-user cluster-admin <username>
```

Example:

```bash
oc adm policy remove-cluster-role-from-user cluster-admin arthur
```

### Determining User Permissions with `who-can`

To investigate whether a user can perform a specific action on a resource, the King can use the `who-can` command:

```bash
oc adm policy who-can <verb> <resource>
```

For example, to check if "arthur" can delete resources:

```bash
oc adm policy who-can delete arthur
```

### Default Cluster Roles

OpenShift comes with a set of default cluster roles that can be assigned to users. These include:

- **admin**
- **basic-user**
- **cluster-admin**
- **cluster-status**
- **edit**
- **self-provisioner**
- **view**

### Adding a Specified Role to a User in a Project

To grant a user a specific role within a project, the King uses the following command:

```bash
oc policy add-role-to-user <role_name> <username> -n <project>
```

For example, to grant "arthur" the "edit" role in the "camelot" project:

```bash
oc policy add-role-to-user edit arthur -n camelot
```

## Conclusion

Wise ruler of the OpenShift kingdom, you now possess the knowledge to manage roles and responsibilities within your domain. By judiciously assigning and revoking roles, you ensure that your kingdom remains well-governed and secure. Remember, the power of delegation is a mighty tool—use it wisely to maintain order and prosperity in your realm.

May your reign be long and your kingdom flourish!

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>