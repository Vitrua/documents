# Kubernetes Networking

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/networking.jpg?raw=true" alt="kubernetes_networking" width="300" height="300">
</div>

## Objective

Learn the intricacies of networking within the mystical realms of Openshift.

## Prerequisites

To embark on this journey of Kubernetes networking, you'll need:

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic understanding of Kubernetes concepts and command-line interfaces (CLI).

## Introduction

Welcome, traveler, to the ethereal realm of Kubernetes networking within the enchanted confines of the Openshift castle. Here, amidst the swirling energies of digital landscapes, lies the essence of seamless communication and load balancing among pods and services. Join us as we unravel the mysteries of Kubernetes networking and delve into the inner workings of the OpenShift Cluster Network Operator.

## Kubernetes Networking

### Services: Anchors in the Digital Seas

In Kubernetes, services serve as anchors in the vast digital seas, providing permanent, static IP addresses for groups of pods belonging to the same deployment or replica set. These services offer load balancing for client requests among member pods, ensuring resilience and reliability within the castle's domains.

#### Creating Services with `oc expose`

To create a service in Openshift, troubleshooters can utilize the `oc expose` command, specifying parameters such as selector, port, target port, and protocol:

```bash
oc expose deployment/<deployment-name> [--selector <selector>] [--port <port>] [--target-port <target port>] [--protocol <protocol>] [--name <name>]
```

#### Viewing Service Endpoints

To view the endpoints associated with a service, troubleshooters can use the `oc get endpoints` command, gaining insights into the connectivity and reachability of pods within the cluster.

### Internal DNS Resolution

Kubernetes employs an internal DNS server, visible only to pods, which assigns DNS names to defined services. These DNS names follow a specific format:

```
SVC-NAME.PROJECT-NAME.svc.CLUSTER-DOMAIN
```

### The OpenShift Cluster Network Operator

The OpenShift Cluster Network Operator (CNO) configures network settings within the Openshift cluster, ensuring seamless integration with Container Network Interface (CNI) plugins. As a cluster administrator, troubleshooters can observe the status of the CNO using commands like `oc get` and `oc describe`.

#### Example Usage

```bash
oc get -n openshift-network-operator deployment/network-operator
oc describe network.config/cluster
```

Embark on this grand journey of Kubernetes networking, as we navigate the digital seas and unravel the mysteries of connectivity and communication within the enchanted confines of the Openshift castle.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>