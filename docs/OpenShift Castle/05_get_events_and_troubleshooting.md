# Unveiling the Mysteries of the Openshift Citadel: Exploring Cluster Events and Troubleshooting

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/detective.jpg?raw=true" alt="events" width="300" height="300">
</div>

## Objective

Delve into the realm of Openshift's cluster events and troubleshooting, illuminating the path to understanding and resolution within the fortress's walls.

## Prerequisites

To embark on this journey of exploration and discovery, you'll need:

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic familiarity with command-line interfaces (CLI) and Kubernetes concepts.

## Introduction

As we venture deeper into the fortified confines of the Openshift citadel, we encounter the realm of cluster events and troubleshooting. Here, amidst the ebb and flow of activity, lies a treasure trove of insights and solutions waiting to be unearthed.

## Get Cluster Events

Adventurers have the power to unveil the chronicles of the cluster through commands like:
```bash
oc get events -n <namespace> --sortby .metadata.creationTimestamp
```
Openshift boasts a monitoring stack anchored by Prometheus, residing within the 'openshift-monitoring' namespace. Powered by the Prometheus platform and Alertmanager, it stands as a sentinel, ever vigilant over the citadel's affairs.

## Check Node Status and Troubleshooting

Armed with knowledge and determination, explorers can scrutinize the general status of the cluster and delve deeper into its inner workings with commands such as:
```bash
oc cluster-info
oc get nodes
oc get node <NODE_NAME> -o jsonpath=*'{"Allocatable:\n"}{.status.allocatable}{"\n\n"}{"Capacity:\n"}{.status.capacity}{"\n"}'
oc get node <NODE_NAME> -o json | jq '.status.conditions'
oc adm node-logs <NODE_NAME> -u <COMPONENT_NAME> --tail 10
```
For those brave enough to seek resolution in the face of adversity, the path of the troubleshooter beckons. Activate the debug session and peer into the heart of the node:
```bash
oc debug node/<NODE_NAME>
```
Within the confines of the debug session, adventurers can confirm the activity of services with commands like:
```bash
# To run binaries in the host's executable path
chroot /host
# To confirm that the services are active
for SERVICES in kubelet crio; do echo ---- $SERVICES ---- ;
systemctl is-active $SERVICES ; echo ""; done
```
Similar procedures can be employed for delving into the workings of pods, unraveling the threads of mystery woven within the citadel's walls.

Embark on this journey of discovery, as we illuminate the shadows cast by the veil of uncertainty, and emerge victorious in the quest for knowledge and resolution within the timeless bastion of Openshift's citadel.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>