# Assigning Administrative Privileges

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/adminprivilege.jpg?raw=true" alt="adminprivilege" width="300" height="300">
</div>

## Objective

Learn how to assign administrative privileges to users and groups in OpenShift using the cluster-admin role, granting them cluster-wide administrative capabilities.

## Prerequisites

- Access to an OpenShift cluster or a terminal emulator connected to one.
- Basic knowledge of OpenShift concepts and command-line interfaces (CLI).

## Introduction

In the grand kingdom of OpenShift, the power to manage the realm lies in the hands of those with administrative privileges. Granting such power is not taken lightly, as it confers the ability to govern the entire cluster. This guide will lead you through the process of assigning the esteemed cluster-admin role to trusted individuals or groups, ensuring the smooth and secure operation of your OpenShift kingdom.

## Assigning Administrative Privileges

### The Cluster-Admin Role

In the heart of the OpenShift castle, the cluster-admin role is akin to the title of High Steward, granting the bearer full administrative rights over the entire realm. This powerful role is essential for managing the kingdom's vast resources and ensuring its defenses are robust.

### Step 1: Identifying Trusted Nobles

Before bestowing such a title, you must identify the noble knights and trusted advisors worthy of this responsibility. These individuals or groups should have a proven track record of loyalty and competence in managing the realm's affairs.

### Step 2: Granting the Cluster-Admin Role

To elevate a user or group to the esteemed position of cluster-admin, use the following command. This command is your royal decree, granting them the necessary powers to govern the kingdom.

```bash
oc adm policy add-cluster-role-to-user cluster-admin <user_name>
```

Replace `<user_name>` with the name of the user or group you wish to elevate. For example, to grant cluster-admin privileges to a user named "arthur", the command would be:

```bash
oc adm policy add-cluster-role-to-user cluster-admin arthur
```

### Step 3: Verifying the Role Assignment

After issuing your decree, it is wise to verify that the privileges have been correctly assigned. You can check the roles assigned to a user with the following command:

```bash
oc get clusterrolebindings | grep <user_name>
```

For instance, to check the roles assigned to "arthur", use:

```bash
oc get clusterrolebindings | grep arthur
```

### Step 4: Removing Administrative Privileges

In the event that a noble knight must be relieved of their duties, the cluster-admin role can be revoked. This ensures the kingdom's security remains intact and only trusted individuals retain administrative powers.

To remove the cluster-admin role from a user, use the following command:

```bash
oc adm policy remove-cluster-role-from-user cluster-admin <user_name>
```

For example, to revoke the cluster-admin privileges from "arthur", the command would be:

```bash
oc adm policy remove-cluster-role-from-user cluster-admin arthur
```

### Best Practices for Managing Administrative Privileges

- **Selective Granting**: Only grant the cluster-admin role to users or groups that require full administrative access.
- **Regular Audits**: Periodically review the roles and privileges assigned to users to ensure compliance with security policies.
- **Training and Awareness**: Ensure that users granted the cluster-admin role are well-trained and aware of their responsibilities and the potential impact of their actions.

## Conclusion

Noble guardian of the OpenShift kingdom, you now possess the knowledge to grant and manage administrative privileges within your realm. By carefully selecting trusted individuals and conferring upon them the cluster-admin role, you ensure that your kingdom is governed by capable and loyal stewards.

As you continue to oversee the prosperous and secure operation of your OpenShift kingdom, remember that the power to manage the realm lies in the hands of those you trust. Use this power wisely, and may your reign be long and successful!

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>