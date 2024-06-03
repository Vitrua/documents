# Managing Self-Provisioning Permissions

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/selfprov.jpg?raw=true" alt="selfprov" width="300" height="300">
</div>

## Objective

Learn to manage self-provisioning permissions in OpenShift to control which users can create new projects, ensuring better governance and resource management.

## Prerequisites

- Access to an OpenShift cluster or a terminal emulator connected to one.
- Basic understanding of OpenShift roles and role bindings.
- Familiarity with Kubernetes Role-Based Access Control (RBAC) concepts.

## Introduction

In the kingdom of OpenShift, the ability for users to create new projects is akin to granting citizens the power to establish new settlements. While this can foster growth and innovation, it also requires oversight to ensure that these new territories are well-planned and do not strain the kingdom's resources. By managing self-provisioning permissions, administrators can control who has the power to create new projects, maintaining order and efficiency within the cluster.

## Managing Self-Provisioning Permissions

By default, the `selfprovisioner` role in OpenShift is bound to all authenticated users, allowing them to create projects. However, to maintain better control and governance, it may be necessary to limit which users can request new projects.

### Viewing Role Bindings

To see the role bindings for the `selfprovisioner` role, use the following command:

```bash
oc describe clusterrolebinding.rbac self-provisioners
```

This command provides details about the role binding, including the subjects (users or groups) that are bound to the role.

### Understanding the Auto-Update Annotation

The `selfprovisioner` role binding includes an `rbac.authorization.kubernetes.io/autoupdate` annotation. This annotation protects roles and bindings from modifications that could interfere with the cluster's operation. When the API server starts, the cluster restores resources with this annotation automatically, unless it is set to `false`.

### Modifying the Role Binding

To effectively edit the subjects in the `selfprovisioner` role binding, follow these steps:

1. **Disable Auto-Update**

   First, disable the auto-update feature for the `selfprovisioner` role binding:

   ```bash
   oc annotate clusterrolebinding/self-provisioners --overwrite rbac.authorization.kubernetes.io/autoupdate=false
   ```

   This command ensures that your modifications will not be overwritten by the cluster's automatic restoration process.

2. **Patch the Role Binding**

   Next, remove the current subjects from the role binding:

   ```bash
   oc patch clusterrolebinding.rbac self-provisioners -p '{"subjects": null}'
   ```

   This command sets the subjects to `null`, effectively removing all users and groups from the `selfprovisioner` role.

### Example Scenario

Imagine the kingdom decides that only members of the royal council should be able to establish new settlements. By following the steps above, the administrator can remove the self-provisioning permissions from all users and then create a new role binding specifically for the council members.

```bash
oc create clusterrolebinding council-self-provisioners --clusterrole=self-provisioner --group=royal-council
```

In this scenario, only users in the `royal-council` group would have the permissions to create new projects, ensuring that new settlements are planned and managed according to the kingdom's guidelines.

## Conclusion

Managing self-provisioning permissions in OpenShift allows administrators to control which users can create new projects. By carefully managing role bindings and leveraging the auto-update annotation, administrators can ensure that only authorized users can establish new projects, maintaining order and efficiency within the cluster. This governance ensures that the kingdom of OpenShift remains well-organized and its resources are used effectively.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>