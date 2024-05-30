# Exposing Non-HTTP Services

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/nonhttp.jpg?raw=true" alt="nonhttp" width="300" height="300">
</div>

## Objective

Expose non-HTTP services in Kubernetes and OpenShift, including the use of Load Balancer services and MetalLB for environments that do not have cloud provider support.

## Introduction

In the kingdom of OpenShift, not all services communicate through the familiar HTTP gateways. Some require their own unique paths, reminiscent of secret tunnels used by messengers in ancient castles. These paths ensure that even non-HTTP protocols can reach their destinations safely and efficiently, much like how the castle's messengers used to navigate through hidden passages.

## Kubernetes Services

To provide transparent access to workload services that run on multiple pods, Kubernetes uses resources of the Service type. These services are akin to the royal messengers, ensuring that messages (network requests) reach their intended recipients (pods) efficiently.

A Kubernetes Service contains the following information:
- A selector that describes the pods running the service.
- A list of the ports that provide the service on the pods.

### Load Balancer Services

In the castle, large-scale announcements were made using the grand balconies, allowing messages to reach everyone. Similarly, load balancer services in Kubernetes act as grand broadcasters for network traffic, ensuring that services are accessible from outside the cluster.

Load balancer services require the use of network features that are not available in all environments. Typically, cloud providers offer their own load balancer services, but what if your castle (cluster) is on bare metal or in a private datacenter?

### MetalLB

For those castles that do not have cloud support, there is MetalLB, a loyal knight ready to provide load balancing services. MetalLB can be installed with the Operator Lifecycle Manager and operates in two modes: Layer 2 and Border Gateway Protocol (BGP). These modes have different properties and requirements, akin to how different types of knights have varying skills and armor.

### Using Load Balancer Services

Once you have configured a Load Balancer component, you can create services of the LoadBalancer type to expose non-HTTP services outside the cluster. This is like assigning a special herald (LoadBalancer service) to ensure your messages get through even the most secure castle walls.

Here is an example of creating a LoadBalancer service:

```yaml title="example_lb.service.yaml"
apiVersion: v1
kind: Service
metadata:
  name: example-lb
  namespace: example
spec:
  ports:
  - port: 1234
    protocol: TCP
    targetPort: 1234
  selector:
    name: example
  type: LoadBalancer
```

After creating the service, you can check the public IP with commands like:

```bash
kubectl get service
oc get example-lb -o jsonpath="{.status.loadBalancer.ingress}"
```

Then use network debugging tools, such as the *ping* and *traceroute* commands, to examine connectivity. These tools act like scouts, ensuring that the paths are clear and the messages can travel without interruption.

## Conclusion

In the realm of OpenShift, exposing non-HTTP services requires a bit more effort, much like navigating secret tunnels in a castle. Whether you use cloud provider load balancers or the MetalLB operator for bare metal clusters, these tools ensure that all your services, HTTP or not, can communicate securely and efficiently. Just as every castle had its unique passages, every OpenShift cluster has its methods for exposing and managing services.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>