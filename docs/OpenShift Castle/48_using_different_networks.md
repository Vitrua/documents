# Using Different Networks

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/diffnet.jpg?raw=true" alt="diffnet" width="300" height="300">
</div>

## Objective

Learn to manage and configure secondary networks in Kubernetes and OpenShift using the Multus CNI plug-in to attach pods to custom networks, both internal and external.

## Prerequisites

- Access to an OpenShift cluster or a terminal emulator connected to one.
- Basic understanding of Kubernetes and OpenShift networking concepts.
- Familiarity with the Multus CNI plug-in and its configuration.
- Knowledge of YAML syntax for creating and editing configuration files.
- Basic command-line skills for using the OpenShift CLI (`oc` commands).

## Introduction

In the kingdom of OpenShift, just as different guilds and factions need their own unique paths and communication channels within the vast castle, sometimes certain pods require their own distinct networks. The Multus CNI plug-in acts like a master architect, creating these specialized pathways to ensure secure and efficient communication for every pod.

## Configuring Secondary Networks

Before you can attach pods to these specialized networks, you must first make these networks available on the cluster nodes. This is akin to laying the groundwork for new secret tunnels within the castle.

### Network Operators

Operators such as Kubernetes NMState or the SR-IOV (Single Root I/O Virtualization) are used to customize node network configurations, ensuring that the infrastructure is in place for these secondary networks.

## Attaching Secondary Networks

Once the groundwork is laid, you can begin attaching pods to these new networks, much like assigning specific guilds to their designated secret passageways.

### NetworkAttachmentDefinition Resource

To configure secondary networks, create a *NetworkAttachmentDefinition* resource or update the cluster network operator configuration to add a secondary network.

### Pod Annotations

Network attachment resources are namespaced, meaning they are available only to pods within their namespace. When additional networks are available, you can add the `k8s.v1.cni.cncf.io/networks` annotation to the pod's template to specify which network to use.

Here is an example of how to annotate a pod to use an additional network:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: example
  namespace: example
spec:
  selector:
    matchLabels:
      app: example
      name: example
  template:
    metadata:
      annotations:
        k8s.v1.cni.cncf.io/networks: example
      labels:
        app: example
        name: example
  spec:
    containers:
    - name: example-container
      image: example-image
```

In this example, the `k8s.v1.cni.cncf.io/networks` annotation is used to attach the pod to the `example` network, much like how a royal decree assigns a guild to a specific tunnel within the castle.

### Checking Network Status

Multus updates the `k8s.v1.cni.cncf.io/networks-status` annotation with the status of the additional networks. You can check the status with the following command:

```bash
oc get pod example -o jsonpath='{.metadata.annotations.k8s\.v1\.cni\.cncf\.io/networks-status}'
```

This is akin to the castle's chief architect reviewing the progress and status of newly constructed secret tunnels, ensuring everything is in order.

## Conclusion

In the realm of OpenShift, managing and configuring secondary networks allows for specialized and secure communication channels, much like the secret tunnels of a grand castle. By using tools like the Multus CNI plug-in, Kubernetes NMState, and SR-IOV, administrators can ensure that every pod has access to the networks it needs, maintaining the efficiency and security of the entire digital kingdom.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>
