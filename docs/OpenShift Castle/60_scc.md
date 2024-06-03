# Security Context Constraints (SCCs)

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/scc.jpg?raw=true" alt="scc" width="300" height="300">
</div>

## Objective

Understand how to use Security Context Constraints (SCCs) in OpenShift to limit access from running pods to the host environment and ensure secure operations within the cluster.

## Prerequisites

- Access to an OpenShift cluster or a terminal emulator connected to one.
- Basic understanding of Kubernetes security concepts, such as SCCs and Role-Based Access Control (RBAC).
- Knowledge of YAML syntax for editing and creating configuration files.

## Introduction

In the fortified kingdom of OpenShift, security is paramount. To protect the realm from potential threats, the castle employs Security Context Constraints (SCCs) as gatekeepers. These SCCs control how pods interact with the host environment, ensuring that only trusted entities have access to sensitive resources.

## Understanding Security Context Constraints (SCCs)

SCCs are security mechanisms in OpenShift that restrict the capabilities of pods, much like royal decrees that limit what different guilds and factions can do within the castle walls. They control access to host resources, ensuring that each pod operates within its assigned boundaries.

### Key Controls of SCCs

SCCs regulate the following aspects of pod behavior:

- **Running Privileged Containers**: Controlling which pods can operate with elevated privileges.
- **Requesting Extra Capabilities for a Container**: Defining what additional capabilities a pod can request.
- **Using Host Directories as Volumes**: Restricting the use of host directories within pods.
- **Changing the SELinux Context of a Container**: Managing how pods can alter their SELinux security context.
- **Changing the User ID**: Controlling the user ID under which a pod operates.

Cluster administrators can list the SCCs defined by OpenShift with the following command:

```bash
oc get scc
```

For detailed information about a specific SCC, use:

```bash
oc describe scc anyuid
```

### Viewing the SCC Used by a Pod

To determine which SCC a pod is using, you can inspect the pod's details. For example, to check the SCC for a specific pod:

```bash
oc describe pod console-5df4fcbb47-67c52 -n openshift-console | grep scc
```

## Managing SCCs

Most pods created by OpenShift use the *restricted-v2* SCC, which provides limited access to resources outside of OpenShift. However, some workloads may require more permissive SCCs. To list all SCCs that can overcome limitations hindering a container:

```bash
oc get deployment <deployment-name> -o yaml | oc adm policy scc-subject-review -f -
```

### Using the *anyuid* SCC

The *anyuid* SCC allows a pod to run as any available user ID in the container, which is useful for containers that need to operate as a specific user. This flexibility is akin to granting a trusted craftsman permission to use any workshop within the castle.

To allow a container to run with a different SCC, follow these steps:

1. **Create a Service Account**: First, create a service account that will be used by the pod. Use the `-n` option to specify the namespace if needed.

    ```bash
    oc create serviceaccount service-account-name -n namespace
    ```

2. **Associate the Service Account with an SCC**: Add the service account to the desired SCC using the `-z` option.

    ```bash
    oc adm policy add-scc-to-user SCC -z <service-account>
    ```

3. **Update the Deployment**: Modify the existing deployment or deployment configuration to use the new service account.

    ```bash
    oc set serviceaccount deployment/<deployment-name> <service-account-name>
    ```

## Conclusion

In the kingdom of OpenShift, SCCs are vital for maintaining the security and integrity of the environment. By understanding and managing SCCs effectively, administrators can ensure that pods operate safely within their designated boundaries, much like ensuring that all guilds and craftsmen within the castle adhere to the king's security protocols. This approach helps maintain a secure and well-functioning realm, protecting both the infrastructure and its inhabitants from potential threats.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>