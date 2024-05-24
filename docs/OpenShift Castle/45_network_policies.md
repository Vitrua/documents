# Network Policies

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/netpol.jpg?raw=true" alt="netpol" width="300" height="300">
</div>

## Objective

Learn to control traffic flow between pods using labels, define specific network policies for secure communication, and implement deny-all policies to enhance security.

## Introduction

In the grand kingdom of OpenShift, maintaining secure and efficient communication between the various inhabitants (pods) is crucial. Network policies act as the kingdom’s intricate system of gates and pathways, controlling traffic flow and ensuring that only the right messages reach their intended destinations. Just as a wise ruler would design a castle with secure passages, OpenShift administrators use network policies to create logical zones within the Software-Defined Network (SDN) that map to their organization’s network zones.

## Understanding Network Policies

Kubernetes network policies control network traffic between pods using labels instead of IP addresses. This means you can separate traffic based on logical groupings, regardless of where the pods are running. To manage communication between pods in different namespaces, you assign labels to the namespaces that need to interact and create network policies to define the allowed traffic.

### Creating Network Policies

Imagine you have two sections in your castle, `network-1` and `network-2`. You want to allow communication between these sections while ensuring only specific traffic is permitted. To achieve this, you assign a label to each namespace and create corresponding network policies.

First, label the namespaces:
```bash
oc label namespace network-1 network=network-1
```

Next, define the network policies. Here are examples of network policies that allow communication between pods in the `network-1` and `network-2` namespaces:

#### Network Policy for `network-1`
```yaml
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
  name: network-1-policy
  namespace: network-1
spec:
  podSelector:
    matchLabels:
      deployment: my-app
  ingress:
  - from:
    - namespaceSelector:
        matchLabels:
          network: network-2
      podSelector:
        matchLabels:
          role: art
    ports:
    - port: 8080
      protocol: TCP
```

#### Network Policy for `network-2`
```yaml
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
  name: network-2-policy
  namespace: network-2
spec:
  podSelector: {}
  ingress:
  - from:
    - namespaceSelector:
        matchLabels:
          network: network-1
```

These policies ensure that only pods in `network-1` with the label `deployment: my-app` can receive traffic from pods in `network-2` with the label `role: art`, and vice versa.

### Boolean Logic in Network Policies

Just as a castle might have different levels of access and security, you can use boolean logic to create more specific network policy rules. This ensures users and applications access only what they should, even between different projects.

## Deny-all Network Policies

In OpenShift, if a pod matches one or more network policies, it only accepts connections allowed by those policies. However, you might want to block all traffic by default and only allow specific communications. This is akin to closing all gates of the castle by default and only opening specific ones when needed.

An empty pod selector applies the policy to all pods in a project. Here’s an example of a policy that blocks all traffic because no ingress rules are defined:

```yaml
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
  name: default-deny
spec:
  podSelector: {}
```

If a pod does not match any network policies, OpenShift does not restrict traffic to that pod. This default behavior ensures that your applications remain accessible unless explicitly restricted.

## Conclusion

Managing network policies in OpenShift is like designing the secure pathways and gates within a castle. By carefully labeling namespaces and creating specific network policies, you ensure secure and efficient communication between pods. Remember to consider the castle’s overall security, not blocking essential services like router pods and monitoring services.

With these strategies, your kingdom of OpenShift will be both secure and well-organized, allowing for seamless and protected communication between all its inhabitants. May your network policies be robust, and your castle gates well-guarded!

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>
