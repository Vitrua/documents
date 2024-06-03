# Pausing the Machine Health Check Resource

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/paures.jpg?raw=true" alt="paures" width="300" height="300">
</div>

## Objective

Learn how to manage the Machine Health Check (MHC) resource during the cluster upgrade process to prevent unnecessary node reboots.

## Prerequisites

- Access to an OpenShift cluster or a terminal emulator connected to one.
- Basic understanding of Machine Health Check (MHC) resources in Kubernetes.
- Familiarity with using `oc` commands to annotate and manage resources.

## Introduction

In the grand kingdom of OpenShift, ensuring the stability and efficiency of worker nodes is paramount to the castle's defense strategy. The Machine Health Check (MHC) acts as vigilant sentries, ever watchful for signs of trouble among the kingdom’s nodes. However, during the upgrade process, nodes may appear temporarily unwell, much like soldiers resting and recovering in the barracks. Just as wise rulers would pause certain security measures during peacetime adjustments to avoid unnecessary alarms, administrators can pause the MHC to prevent it from mistaking these temporary states for serious issues, thereby avoiding unnecessary reboots.

## Steps to Pause and Resume Machine Health Check

Pausing the MHC ensures that worker nodes are not rebooted during the upgrade, allowing for a smooth and uninterrupted update process. Think of this as a royal decree to temporarily ease the watchful eyes of the sentries, ensuring that their well-meaning but potentially disruptive interventions are paused.

### Listing Available Machine Health Check Resources

First, gather intelligence on the available MHC resources within the `openshift-machine-api` namespace. This step is akin to consulting the royal records to understand the current state of castle defenses before making any strategic changes.

```bash
oc get machinehealthcheck -n openshift-machine-api
```

### Pausing the Machine Health Check Resource

Next, issue a royal decree to pause the MHC resource by adding the `cluster.x-k8s.io/paused` annotation. This annotation acts like a temporary truce, instructing the sentries to stand down and refrain from taking action during the upgrade.

```bash
oc annotate machinehealthcheck -n openshift-machine-api machine-api-termination-handler cluster.x-k8s.io/paused=""
```

### Example Command

For instance, to pause the MHC resource named `machine-api-termination-handler`, the command is:

```bash
oc annotate machinehealthcheck -n openshift-machine-api machine-api-termination-handler cluster.x-k8s.io/paused=""
```

### Resuming the Machine Health Check Resource

Once the cluster upgrade is complete, remove the `cluster.x-k8s.io/paused` annotation to lift the truce and allow the MHC to resume its vigilant watch. This is akin to ending the temporary ceasefire, enabling the sentries to return to their full duties in safeguarding the castle.

```bash
oc annotate machinehealthcheck -n openshift-machine-api machine-api-termination-handler cluster.x-k8s.io/paused-
```

### Example Command

To resume the MHC resource named `machine-api-termination-handler`, the command is:

```bash
oc annotate machinehealthcheck -n openshift-machine-api machine-api-termination-handler cluster.x-k8s.io/paused-
```

## Conclusion

By effectively managing the Machine Health Check resource during the upgrade process, you ensure that your OpenShift kingdom remains stable and efficient, much like a well-defended castle avoiding unnecessary disturbances. Pausing the MHC resource temporarily prevents the misinterpretation of node unavailability as critical issues, thereby maintaining a smooth and uninterrupted upgrade process. The wise rulers of OpenShift know that sometimes, a strategic pause is the best way to ensure long-term stability and peace in their realm.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>