# Network Attachment Custom Resource

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/netattach.jpg?raw=true" alt="netattach" width="300" height="300">
</div>

## Objective

Understand how to create and use NetworkAttachmentDefinition resources in Kubernetes and OpenShift for different types of network interfaces such as host device, bridge, IPVLAN, and MACVLAN.

## Prerequisites

- Access to an OpenShift cluster or a terminal emulator connected to one.
- Basic understanding of Kubernetes CNI (Container Network Interface) plug-ins.
- Familiarity with different network attachment types such as host device, bridge, IPVLAN, and MACVLAN.
- Knowledge of YAML syntax for creating and editing configuration files.
- Basic command-line skills for using the OpenShift CLI (`oc` commands).

## Introduction

In the kingdom of OpenShift, different guilds and factions often require specialized communication channels. The NetworkAttachmentDefinition resource acts as the master plan, detailing the construction and connection of these unique pathways. Each type of network interface serves a distinct purpose, ensuring that every guild can communicate effectively within the vast castle.

## Types of Network Attachment Definitions

### Host Device

The host device type attaches a network interface directly to a single pod. This is akin to giving a messenger a direct, private passageway to ensure their messages are delivered without interference.

### Bridge

The bridge type utilizes an existing bridge interface on the node or sets up a new bridge interface. Pods attached to this network can communicate with each other through the bridge and with any other networks attached to the bridge. This is like constructing a new courtyard where guilds can gather and interact freely.

### IPVLAN

The IPVLAN type establishes a network attached to a network interface using IPVLAN. This configuration allows for efficient network communication by segmenting traffic based on IP addresses, much like having separate hallways for different guilds within the castle.

### MACVLAN

The MACVLAN type establishes a network attached to a network interface using MAC addresses. This is similar to having dedicated pathways for specific guild members, ensuring secure and efficient communication.

## Example: NetworkAttachmentDefinition for a Host Device

Here is an example of a *NetworkAttachmentDefinition* resource for a host device:

```yaml
apiVersion: k8s.cni.cncf.io/v1
kind: NetworkAttachmentDefinition
metadata:
  name: example
spec:
  config: |-
  {
    "cniVersion": "0.3.1",
    "name": "example",
    "type": "host-device",
    "device": "ens4",
    "ipam": {
      "type": "dhcp"
    }
  }
```

### Explanation

- **apiVersion**: Specifies the API version for the resource.
- **kind**: Defines the type of resource, in this case, NetworkAttachmentDefinition.
- **metadata**: Contains metadata for the resource, such as the name.
- **spec**: Defines the configuration for the network attachment.
    - **cniVersion**: Specifies the CNI (Container Network Interface) version.
    - **name**: Names the network.
    - **type**: Defines the type of network, here it is `host-device`.
    - **device**: Specifies the network device to attach, e.g., `ens4`.
    - **ipam**: Configures the IP address management, here it uses DHCP.

This setup is like providing a dedicated and secure passageway for a specific guild member, ensuring they have direct access to their destination.

## Conclusion

In the realm of OpenShift, creating and configuring NetworkAttachmentDefinition resources allows for the establishment of specialized and efficient communication channels. Whether using host devices, bridges, IPVLAN, or MACVLAN, these custom resources ensure that every pod has the network access it needs. By mastering these configurations, administrators can maintain the efficiency and security of the entire digital kingdom, ensuring smooth and effective communication throughout the castle.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>