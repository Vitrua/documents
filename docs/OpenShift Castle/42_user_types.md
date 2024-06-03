# User Types

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/usertypes.jpg?raw=true" alt="usertypes" width="300" height="300">
</div>

## Objective

Learn the different types of users in Red Hat OpenShift Container Platform (RHOCP) and their unique roles within the system. You'll learn about regular users, system users, and service accounts, understanding their responsibilities and how to manage them effectively. Finally ensure that they have the appropriate permissions and access levels within your OpenShift environment.

## Prerequisites

- Access to an OpenShift cluster or a terminal emulator connected to one.
- Basic understanding of OpenShift user roles and permissions.
- Familiarity with OpenShift CLI (`oc` commands) and user management concepts.

## Introduction

In the kingdom of OpenShift, every citizen, be it a valiant knight, a humble farmer, or a diligent scribe, plays a vital role in maintaining the harmony and prosperity of the realm. Similarly, every interaction within the OpenShift platform is associated with a specific type of user. These users, much like the inhabitants of a bustling medieval castle, have distinct roles and responsibilities.

This guide will introduce you to the different types of users in OpenShift and their unique roles within the system.

## User Types

OpenShift recognizes three primary types of users:

1. **Regular Users**
2. **System Users**
3. **Service Accounts**

### 1. Regular Users

**Regular users** are the knights, nobles, and citizens of the OpenShift kingdom. They are the interactive users who access the platform to perform various tasks and activities. These users are represented by the User object in OpenShift and have specific permissions and access levels based on their roles.

In the castle, regular users are like the advisors and artisans who interact directly with the king, providing counsel and crafting essential items for the kingdom's prosperity. They might create new applications, manage resources, or perform administrative tasks.

Example command to list regular users:
```bash
oc get users
```

### 2. System Users

**System users** are the unsung heroes who work tirelessly behind the scenes to ensure the kingdom runs smoothly. These users are automatically created for infrastructure interactions, such as a cluster administrator or per-node users. Their names start with the "system:" prefix, indicating their special status.

In the castle, system users are like the castle's keepers and sentinels. They ensure the castle's defenses are strong, the gates are functioning, and all mechanisms are in perfect working order. They handle the critical, automated tasks that keep the platform running seamlessly.

Example of a system user name:
```bash
system:admin
```

### 3. Service Accounts

**Service accounts** are the specialized entities associated with projects. They are used by workloads to invoke Kubernetes APIs and perform automated tasks. Service accounts are created automatically by the system or by project administrators and have names that start with the "system:serviceaccount:" prefix.

In the castle, service accounts are like the royal messengers and envoys who carry out specific missions on behalf of the kingdom. They perform tasks such as deploying applications, managing secrets, and ensuring that workloads have the necessary permissions to operate effectively.

Example of a service account name:
```bash
system:serviceaccount:my-project:default
```

## Managing User Types

Understanding the different types of users is crucial for effective management and security in OpenShift. Just as a wise king must know the roles of his subjects, an OpenShift administrator must know how to manage these user types.

### Creating and Managing Regular Users

Regular users can be created and managed using identity providers. For example, using the HTPasswd identity provider, you can create and manage user credentials.

### Managing System Users

System users are automatically created and managed by OpenShift. They perform essential infrastructure tasks and typically do not require manual intervention.

### Creating and Managing Service Accounts

Service accounts are created automatically when a new project is created. However, administrators can also create custom service accounts for specific tasks.

Example command to create a service account:
```bash
oc create serviceaccount my-service-account
```

### Assigning Roles to Users

To ensure that each user type has the appropriate permissions, roles can be assigned using the `oc adm policy` command.

Example command to assign a role to a user:
```bash
oc adm policy add-role-to-user edit my-user -n my-project
```

## Conclusion

In the kingdom of OpenShift, every user type plays a crucial role in maintaining the harmony and efficiency of the system. Whether they are regular users, system users, or service accounts, understanding their roles and managing their permissions is key to ensuring a secure and well-functioning platform.

As the ruler of this digital realm, your knowledge of these user types will help you govern wisely, ensuring that each citizen of your kingdom performs their duties effectively and securely. May your reign be prosperous and your kingdom thrive!

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>
