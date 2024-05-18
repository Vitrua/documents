# Compute Resources

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/cresources.jpg?raw=true" alt="compute_resources" width="300" height="300">
</div>

## Objective

Learn how to define and manage compute resources for your containers in Openshift, ensuring efficient and optimal use of CPU and memory.

## Prerequisites

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic understanding of Openshift concepts and command-line interfaces (CLI).

## Introduction

Welcome, esteemed guardian of resources! In the fortified castle of Openshift, you hold the power to allocate and manage the kingdom's precious resources. By defining resource requests and limits for your application containers, you ensure that each subject receives their fair share, preventing any single container from hoarding the castle’s CPU and memory. Join us as we explore the art of managing compute resources, safeguarding the balance and efficiency of your applications within the Openshift kingdom.

## Understanding Compute Resources

### The Lifeblood of Your Applications

In the magical realm of Openshift, compute resources are the lifeblood of your applications. Just as each knight in the castle requires provisions to maintain their strength, each container needs CPU and memory to function effectively. By setting resource requests and limits, you ensure that every container receives the necessary resources while preventing any from consuming too much.

- **Resource Requests**: The amount of CPU and memory guaranteed for a container.
- **Resource Limits**: The maximum amount of CPU and memory a container can use.

## Configuring Compute Resources

### Allocating Provisions for Your Knights

To allocate resources for your containers, you can define resource requests and limits using YAML files or the CLI.

#### Example Usage with YAML

Here’s how to configure resource requests and limits for a container:

```yaml title="compute-resources-example.yaml"
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-nginx-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: my-nginx
  template:
    metadata:
      labels:
        app: my-nginx
    spec:
      containers:
      - name: my-nginx
        image: nginx
        resources:
          requests:
            cpu: "1000m"
            memory: "1Gi"
          limits:
            cpu: "200m"
            memory: "1Gi"
```

In this example, the container named "my-nginx" requests 1000 millicores (1 CPU) and 1Gi of memory, with limits set to 200 millicores and 1Gi of memory. Apply this configuration using the command:

```bash
oc create -f compute-resources-example.yaml
```

#### Configuring Resources via CLI

You can also set resource requests and limits directly through the CLI. For example, to set resources for a deployment named "my-nginx":

```bash
oc set resources deployment my-nginx --requests cpu=1000m,memory=1Gi --limits cpu=200m,memory=1Gi
```

### Monitoring and Managing Resources

To view the available and used resources of a node:

```bash
oc describe node <node_name>
```

To check the resource usage of a node:

```bash
oc adm top node <node_name>
```

To see the resource usage of all pods in a specific namespace:

```bash
oc adm top pods -n <namespace_name>
```

## Limit Compute Resources

### Preventing Resource Hoarding

By setting resource limits, you prevent any container from consuming excessive resources, ensuring fair distribution and maintaining the kingdom's harmony.

#### Example Usage with YAML

To limit resources for a container, you define the limits section in the YAML file:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-nginx-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: my-nginx
  template:
    metadata:
      labels:
        app: my-nginx
    spec:
      containers:
      - name: my-nginx
        image: nginx
        resources:
          requests:
            cpu: "100m"
            memory: "1Gi"
          limits:
            cpu: "200m"
            memory: "1Gi"
```

If the container exceeds its memory limit, it will be terminated by the Out Of Memory (OOM) killer. If it exceeds its CPU limit, it will be throttled, slowing down its execution.

#### Configuring Limits via CLI

To set limits using the CLI:

```bash
oc set resources deployment/my-app --limits memory=1Gi
oc set resources deployment/my-app --limits cpu=200m
```

## Conclusion

Embark on the journey of mastering compute resources within the fortified bastion of Openshift. By understanding and configuring resource requests and limits, you ensure fair and efficient allocation of CPU and memory, maintaining the balance and harmony of your applications within the mystical confines of Openshift.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>