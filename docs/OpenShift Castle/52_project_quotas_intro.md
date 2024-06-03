# Apply and Troubleshoot Project Quotas

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/projquot.jpg?raw=true" alt="projquot" width="300" height="300">
</div>

## Objective

Learn to apply and manage project quotas in OpenShift using both the web console and command-line interface to ensure efficient resource utilization and adherence to organizational policies.

## Prerequisites

- Access to an OpenShift cluster or a terminal emulator connected to one.
- Basic understanding of Kubernetes and OpenShift resource management and quota concepts.
- Familiarity with both the OpenShift web console and command-line interface.
- Knowledge of YAML syntax for creating and editing configuration files.
- Basic command-line skills for using the OpenShift CLI (`oc` commands).

## Introduction

In the kingdom of OpenShift, administrators must ensure that resources are allocated fairly among the various guilds (projects) to maintain harmony and efficiency. Project quotas serve as the laws that dictate how much of each resource a guild can consume, preventing any single guild from monopolizing the kingdom's resources.

## Applying Project Quotas

Administrators can apply project quotas using the OpenShift web console or the command-line interface, ensuring flexibility and ease of management.

### Using the Web Console

Navigate to **Administration** > **ResourceQuotas** to create a resource quota from the web console. This method provides a user-friendly interface for managing quotas, much like how a royal scribe would use a detailed ledger to record resource allocations. The web console acts as a grand chamber where the kingdom's overseers (administrators) can decree the resource limits for each guild.

### Using the Command-Line Interface

Alternatively, you can use the `oc create resourcequota` command to create a resource quota. For example:

```bash
oc create resourcequota example --hard=count/pods=1
```

This command is like issuing a royal decree that sets the boundaries for resource usage within a guild, ensuring no guild can hoard resources at the expense of others.

### Example Explanation

- **oc create resourcequota example**: Creates a resource quota named `example`.
- **--hard=count/pods=1**: Sets a hard limit of 1 pod for this quota, ensuring that only one pod can be created within the project. This is akin to granting a guild permission to use a single workshop within the castle walls.

### Retrieving Quota Information

After creating a resource quota, you can retrieve information about its status with commands like:

```bash
oc get quota example -o yaml
oc get quota
```

These commands allow you to view detailed information about the resource quotas, much like how the royal scribe reviews the resource ledger to ensure compliance with the kingdom's laws. The status of these quotas reflects the real-time usage and availability of resources within the kingdom.

## Troubleshooting Resource Quotas

Resource quotas in Kubernetes are extensible, meaning that Kubernetes cannot always verify if a resource quota is correct. This can lead to scenarios where a quota command is issued but not effectively enforced, without providing negative feedback.

### Ensuring Correct Quotas

To ensure a quota is correctly applied, you can create a quota with an artificially low value in a testing environment. This approach allows you to generate an error as soon as the quota is exceeded, confirming that the quota is being enforced as expected. It's like testing a new law in a small part of the kingdom before rolling it out across all the guilds.

For example, set a low quota value and attempt to exceed it:

```bash
oc create resourcequota test-quota --hard=cpu=1m
```

Then, create a resource that requests more than 1 millicore of CPU:

```bash
oc run test-pod --image=busybox --requests=cpu=10m -- /bin/sh -c "sleep 1000"
```

If the quota is correctly enforced, you should receive an error indicating that the resource creation failed due to exceeding the quota. This trial and error process ensures that the kingdom's laws are fair and effective.

In the kingdom of OpenShift, this is akin to the royal guards (administrators) setting up a trial scenario in the castle courtyard to test if the newly issued laws are effective. By observing the reactions (errors) when the laws are broken, they can ensure that the rules are robust and enforceable, maintaining order and fairness in the realm.

## Conclusion

Applying and managing project quotas in OpenShift ensures that resources are allocated fairly and efficiently among projects. By using the web console or command-line interface, administrators can easily create and monitor resource quotas, maintaining harmony within the digital kingdom. Troubleshooting techniques, such as setting low quotas in a test environment, help verify that quotas are correctly enforced, ensuring smooth and effective resource management. Just as a well-governed kingdom thrives on fair laws and resource management, an efficiently managed OpenShift cluster ensures optimal performance and resource utilization.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>