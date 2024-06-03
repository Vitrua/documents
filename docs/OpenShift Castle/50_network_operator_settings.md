# Network Operator Settings

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/netop.jpg?raw=true" alt="netop" width="300" height="300">
</div>

## Objective

Learn how to create network attachments by editing the cluster network operator configuration in OpenShift, including configuring IP Address Management (IPAM) settings for custom networks.

## Prerequisites

- Access to an OpenShift cluster or a terminal emulator connected to one.
- Understanding of Kubernetes networking and CNI plug-ins.
- Familiarity with OpenShift's network operator and its configuration.
- Knowledge of YAML syntax for creating and editing configuration files.
- Basic command-line skills for using the OpenShift CLI (`oc` commands).

## Introduction

In the kingdom of OpenShift, the network operator acts like the castle's chief engineer, overseeing and managing the intricate web of pathways that connect different guilds and factions. By configuring the network operator, administrators can establish new custom networks, ensuring that every pod has the network access it needs, much like creating new secret tunnels within the castle walls.

## Creating Network Attachments through Network Operator Configuration

To create a network attachment, you can edit the cluster network operator configuration. This method allows you to define additional networks in a centralized manner, ensuring that all nodes and pods have access to these custom pathways.

### Example Configuration

Here is an example of how to create a network attachment by editing the cluster network operator configuration:

```yaml
apiVersion: operator.openshift.io/v1
kind: Network
metadata:
  name: cluster
spec:
  ...
  additionalNetworks:
  - name: example
    namespace: example
    rawCNIConfig: |-
      {
        "cniVersion": "0.3.1",
        "name": "example",
        "type": "host-device",
        "device": "ens4",
        "ipam": {
          "type": "dhcp"
        }
      }
    type: Raw
```

### Explanation

- **apiVersion**: Specifies the API version for the resource.
- **kind**: Defines the type of resource, in this case, Network.
- **metadata**: Contains metadata for the resource, such as the name (`cluster`).
- **spec**: Defines the specifications for the network configuration.
    - **additionalNetworks**: Lists the additional networks to be configured.
        - **name**: Names the additional network.
        - **namespace**: Specifies the namespace where the network will be available.
        - **rawCNIConfig**: Provides the raw CNI configuration in JSON format.
        - **type**: Specifies the type of network configuration, here it is `Raw`.

This configuration is like the chief engineer's blueprint for a new tunnel, detailing every aspect from the tunnel's entrance to its path through the castle.

## Configuring IP Address Management (IPAM)

The IPAM CNI plug-in provides IP addresses for other CNI plug-ins. In the previous example, the *ipam* key contains a network configuration that uses DHCP. However, you can provide more complex network configurations in the *ipam* key.

### Using Static IP Addresses

For example, here is how you can configure a static IP address:

```yaml
"ipam": {
  "type": "static",
  "addresses": [
    {"address": "192.168.X.X/24"}
  ]
}
```

This configuration assigns a static IP address to the network interface, much like assigning a permanent residence to a specific guild member within the castle.

### Flexibility in Network Configuration

You can define more than one additional network for your cluster, giving you flexibility when configuring pods that deliver network functions. This is akin to constructing multiple secret tunnels within the castle, each serving a unique purpose and ensuring efficient communication across the kingdom.

## Conclusion

In the realm of OpenShift, configuring network attachments through the network operator allows administrators to create and manage custom networks efficiently. By utilizing IPAM settings, whether through DHCP or static IP addresses, you can ensure that every pod has the network access it needs. This centralized approach to network configuration is essential for maintaining the efficiency and security of the entire digital kingdom.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>