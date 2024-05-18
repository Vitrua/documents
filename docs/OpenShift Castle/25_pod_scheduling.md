
# Pod Scheduling

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/podscheduling.jpg?raw=true" alt="podscheduling" width="300" height="300">
</div>

## Objective

Understand the intricacies of pod scheduling within the Openshift cluster, ensuring efficient and optimal placement of your applications.

## Prerequisites

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic knowledge of Openshift concepts and command-line interfaces (CLI).

## Introduction

Greetings, master scheduler of the mystical realm! Within the fortified bastion of Openshift, the pod scheduler acts as the wise overseer, orchestrating the placement of your application pods onto the nodes of your cluster. As the steward of resource allocation, you wield the power to filter, prioritize, and select the best nodes, ensuring that your applications run efficiently and reliably. Join us on a journey to uncover the secrets of pod scheduling and master the art of optimal pod placement.

## Understanding Pod Scheduling

### The Orchestration of Resource Allocation

In the enchanted world of Openshift, pod scheduling is akin to assigning the best quarters to your loyal subjects within the castle. This process involves three main steps:

1. **Filtering Nodes**: The scheduler evaluates which nodes are suitable based on the criteria specified by the pods, such as node selectors and resource requests for CPU, memory, and storage. Only the nodes meeting these requirements are considered eligible. If no eligible nodes are found, a FailedScheduling event is triggered, indicating that no suitable quarters are available.

2. **Prioritizing Nodes**: Among the eligible nodes, the scheduler assigns weighted scores based on various criteria, determining their suitability for hosting the pod. Nodes with higher scores are considered better candidates.

3. **Selecting the Best Fit Node**: The scheduler sorts the nodes by their scores and selects the highest-scoring node to host the pod. If multiple nodes share the highest score, the scheduler employs a round-robin method to choose one. Once a suitable node is selected, a Scheduled event is generated for the pod.

## Configuring Pod Scheduling

### Crafting the Perfect Quarters

To ensure your applications are allocated the best quarters within the castle, you can customize the scheduling process by defining specific criteria.

#### Example Usage with Node Selectors and Resource Requests

Here’s how to configure a pod with specific node selectors and resource requests:

```yaml title="pod-scheduling-example.yaml"
apiVersion: v1
kind: Pod
metadata:
  name: my-app-pod
spec:
  containers:
  - name: my-app-container
    image: my-app:latest
    resources:
      requests:
        memory: "64Mi"
        cpu: "250m"
  nodeSelector:
    disktype: ssd
```

In this example, the pod named "my-app-pod" requests specific CPU and memory resources and is scheduled to nodes labeled with `disktype=ssd`. Apply this configuration using the command:

```bash
oc create -f pod-scheduling-example.yaml
```

#### Customizing Scheduling via CLI

You can also set node selectors and resource requests directly through the CLI. For example, to schedule a pod with specific criteria:

```bash
oc run my-app-pod --image=my-app:latest --requests=cpu=250m,memory=64Mi --overrides='{ "apiVersion": "v1", "spec": { "nodeSelector": { "disktype": "ssd" } } }'
```

## Conclusion

Embark on the journey of mastering pod scheduling within the fortified bastion of Openshift. By understanding and configuring the scheduling process, you ensure your applications are efficiently and reliably allocated the best quarters, maintaining their performance and resilience within the mystical confines of Openshift.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>